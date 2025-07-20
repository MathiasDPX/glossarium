<script lang="ts">
export let items: { id: string; label: string }[] = [];
</script>

<ul class="flex text-sm text-yellow-900">
    {#each items as item (item.id)}
    <li class={items.indexOf(item) === 0 ? "" : "ml-4"}>
        <a href="#{item.id}" class="hover:underline transition-all duration-200 hover:text-yellow-700">
            {item.label}
        </a>
    </li>
    {/each}
</ul>