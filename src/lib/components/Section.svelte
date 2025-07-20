<script>
export let id;
export let title;
export let bgClass = '';
export let containerClass = 'max-w-4xl mx-auto';
</script>

<section {id} class="py-20 px-6 {bgClass}">
    <div class="{containerClass} text-center">
        <h2 class="text-3xl font-semibold text-yellow-900 mb-6">{title}</h2>
        <slot />
    </div>
</section>