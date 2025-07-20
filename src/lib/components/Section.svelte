<script lang="ts">
export let id :string;
export let title :string;
export let bgClass :string = '';
export let containerClass :string = 'max-w-4xl mx-auto';
</script>

<section {id} class="py-20 px-6 {bgClass}">
    <div class="{containerClass} text-center">
        <h2 class="text-3xl font-semibold text-yellow-900 mb-6">{title}</h2>
        <slot />
    </div>
</section>