# How to host a Flask app on Nest

As an example, I will use an example app that you can find in the `app` subfolder. But you can use any app that uses Flask. Before starting, I assume you are logged into Nest with your repository is cloned

### Virtual environment

Begin by creating a virtual environment in your project directory:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
pip install waitress
```

This creates a `.venv` folder, activates the environment, and installs the dependencies listed in `requirements.txt`.  
The last command ensures `waitress` is installed if it's not already specified in your requirements.

### Systemd

We'll use a systemd service to ensure our app starts automatically when Nest boots up and has proper logging.

```toml
# ~/.config/systemd/user/test.service

[Unit]
Description=Test app
After=network-online.target

[Service]
WorkingDirectory=%h/test
ExecStart=%h/test/.venv/bin/waitress-serve --trusted-proxy="*" --trusted-proxy-headers="x-forwarded-for" --unix-socket="/run/user/%U/test.sock" --threads 20 main:app

[Install]
WantedBy=default.target
```

Let's break this down. The service file is split into three sections:

1. `Unit`: sets up metadata and dependencies.
2. `Service`: defines how the service runs, its environment, and behavior.
3. `Install`: controls how and when the service should be enabled.

The `Description` and `WorkingDirectory` are self-explanatory.  
- `After`: ensures the network is up by waiting for `network-online.target`.
- `WantedBy`: hooks into `default.target`, which comes after the network and before the graphical target (since Nest supports RDP).

Now, let's look more closely at `ExecStart` since it's the heart of our service:  
- We're using waitress from our virtual environment.
- The `trusted-proxy` and `trusted-proxy-headers` options are set because traffic will go through Caddy, and we want to preserve the real client IP instead of just seeing localhost.
- We're telling waitress to use a Unix socket instead of a port. This helps prevent someone from "stealing" our port or proxying it through the Nest CLI.
- To speed things up, we increase the number of threads that waitress uses (default is 4, we're using 20).
- Finally, we specify `main:app`, meaning waitress will look for the `app` variable in `main.py`.

Notice I didn't use a hardcoded path like `/home/mathias/test`, but `%h/test` instead. This is a systemd specifier, which gets resolved to the right value at runtime. Specifiers can handle things like user group, architecture, UID, and [more](https://www.freedesktop.org/software/systemd/man/latest/systemd.unit.html#Specifiers).

After creating your service you can start & enable it with  `systemctl --user enable --now test`

### Caddy

Next, you'll connect your domain (`your.domain`) to the service you just created.

First, exit your virtual environment and return to your home directory:

```bash
deactivate && cd ~
```

Tell the main Caddy instance to route `your.domain` to your user Caddy instance:

```bash
nest caddy add your.domain
```

Before editing your Caddyfile, find your UID:

```bash
echo $UID
```

Add the following to your Caddyfile, replacing `your.domain` and `$UID` as needed:

```caddyfile
http://your.domain {
    bind unix/.your.domain.webserver.sock|777
    reverse_proxy unix//run/user/$UID/test.sock {
        header_up X-Forwarded-For {header.X-Forwarded-For}
    }
}
```

Finally, restart Caddy to apply the changes:

```bash
systemctl --user restart caddy
```

Your Flask app should now be accessible at your domain!

### Sources
1. [systemd.unit - freedesktop.org](https://www.freedesktop.org/software/systemd/man/latest/systemd.unit.html)
2. [systemd.service - freedesktop.org](https://www.freedesktop.org/software/systemd/man/latest/systemd.service.html)
3. [Maitriser la gestion des services Linux avec systemd - stephane-robert.info](https://blog.stephane-robert.info/docs/admin-serveurs/linux/services/)