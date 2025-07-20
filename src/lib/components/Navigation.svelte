<script>
export let items = [];
</script>

<ul class="flex space-x-4 text-sm text-yellow-900">
    {#each items as item}
    <li>
        <a href="#{item.id}" class="hover:underline transition-all duration-200 hover:text-yellow-700">
            {item.label}
        </a>
    </li>
    {/each}
</ul>