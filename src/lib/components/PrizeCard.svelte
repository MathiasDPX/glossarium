<script lang="ts">
export let href: string;
export let src: string;
export let alt: string;

$: if (!src && href) {
    src = `${href}/cover.jpg`;
}
</script>

<a target="_blank" {href} class="inline-block mx-5 group">
    <img 
    {src} 
    {alt} 
    class="w-auto h-60 rounded shadow-md duration-300" 
    />
</a>