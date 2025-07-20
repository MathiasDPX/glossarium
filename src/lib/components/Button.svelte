<script lang="ts">
export let href :string;
export let target :string = '_blank';

$: buttonClasses = 'bg-yellow-900 text-white hover:bg-yellow-800';
</script>

<a 
{href} 
{target} 
class="inline-block px-6 py-3 rounded-full text-lg font-medium transition-all duration-300 transform hover:scale-105 {buttonClasses}"
>
<slot />
</a>