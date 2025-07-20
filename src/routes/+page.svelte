<script>
import Navigation from '$lib/components/Navigation.svelte';
import Section from '$lib/components/Section.svelte';
import IdeaItem from '$lib/components/IdeaItem.svelte';
import PrizeCard from '$lib/components/PrizeCard.svelte';
import Button from '$lib/components/Button.svelte';

const navItems = [
    { id: 'about', label: 'About' },
    { id: 'ideas', label: 'Ideas' },
    { id: 'prizes', label: 'Prizes' },
    { id: 'rsvp', label: 'RSVP' }
];

const ideas = [
    { icon: '📜', text: 'How to make your first terminal app' },
    { icon: '💾', text: 'Demystifying how filesystems work' },
    { icon: '⚙️', text: 'An illustrated guide to CPU registers' },
    { icon: '🕊️', text: 'How to free yourself from Windows Spywares' },
    { icon: '👣', text: 'First steps with Svelte' },
    { icon: '➕', text: 'And so much more!' }
];

const prizes = [
    {
        href: 'https://store.wizardzines.com/products/how-git-works',
        src: 'https://store.wizardzines.com/cdn/shop/files/HowGitWorksColor-RGB-Web_1024x1024@2x.jpg?v=1716911764',
        alt: 'How Git Works'
    },
    {
        href: 'https://store.wizardzines.com/products/how-integers-and-floats-work',
        src: 'https://store.wizardzines.com/cdn/shop/files/HowIntegersAndFloatsWorkCMYK300dpi_1024x1024@2x.jpg?v=1686929974',
        alt: 'How Integers And Floats Work'
    },
    {
        href: 'https://store.wizardzines.com/products/the-pocket-guide-to-debugging',
        src: 'https://images-na.ssl-images-amazon.com/images/S/compressed.photo.goodreads.com/books/1672175555i/75355942.jpg',
        alt: 'The Pocket Guide to Debugging'
    },
    {
        href: 'https://store.wizardzines.com/products/how-dns-works',
        src: 'https://jvns.ca/images/dns-cover.png',
        alt: 'How DNS Works'
    }
];
</script>

<!-- Navbar -->
<nav class="fixed top-0 w-full bg-[#f9f6ec] shadow z-50 border-b border-gray-300">
    <div class="max-w-7xl mx-auto px-4 py-3 flex justify-between items-center">
        <span class="text-2xl font-bold text-yellow-900 tracking-wide">Glossarium</span>
        <Navigation items={navItems} />
    </div>
</nav>

<!-- Hero Section -->
<section class="h-screen flex flex-col justify-center items-center text-center px-6 pt-20">
    <h1 class="text-6xl md:text-7xl font-extrabold text-yellow-900 mb-4 tracking-wider">Glossarium</h1>
    <p class="text-2xl md:text-3xl text-yellow-800 italic">Sharing is caring</p>
</section>

<!-- About Section -->
<section id="about" class="max-w-3xl mx-auto px-6 py-20 text-center">
    <h2 class="text-4xl font-semibold text-yellow-900 mb-6">What is Glossarium?</h2>
    <p class="text-lg mb-4 leading-relaxed text-gray-700">
        <strong>Glossarium</strong> is a celebration of shared knowledge. You write a tutorial — a how-to, an explainer, a personal guide —
        and we'll reward your wisdom with access to every zines by <a href="https://wizardzines.com" target="_blank" class="text-yellow-800 underline">Julia Evans</a>.
    </p>
    <span class="text-lg italic text-yellow-900">Knowledge is power. Information is liberating. Education is the premise of progress, in every society, in every family.</span><span class="text-lg text-yellow-900"> - Kofi Annan</span>
</section>

<!-- Ideas Section -->
<Section id="ideas" title="What can you share?" bgClass="bg-[#f6f1e7]">
    <ul class="space-y-4 text-left text-lg max-w-xl mx-auto">
        {#each ideas as idea}
        <IdeaItem icon={idea.icon} text={idea.text} />
        {/each}
    </ul>
</Section>

<!-- Prizes Section -->
<Section id="prizes" title="What you will get" containerClass="mx-auto">
    <div class="overflow-x-auto whitespace-nowrap">
        {#each prizes as prize}
        <PrizeCard href={prize.href} src={prize.src} alt={prize.alt} />
        {/each}
    </div>
    <p class="mt-6 text-gray-700 italic">You will get all of them!</p>
</Section>

<!-- RSVP Section -->
<section id="rsvp" class="bg-[#f3ede0] py-20 px-6 text-center">
    <h2 class="text-3xl font-semibold text-yellow-900 mb-6">Ready to share?</h2>
    <p class="text-lg mb-4 text-gray-800">Submit your tutorial and get access to all zines.<br><i><small>You need to be 18 or younger.</small></i></p>
    <Button href="https://forms.hackclub.com/home">RSVP Now</Button>
</section>

<!-- Footer -->
<footer class="bg-[#f9f6ec] py-6 text-center text-sm text-gray-600 border-t border-gray-300">
    <p>Made with love and scrolls by @<a href="https://github.com/MathiasDPX" class="underline">mathias</a> 📚</p>
    <p>
        Source on <a href="https://github.com/MathiasDPX/glossarium" class="underline">GitHub</a> • Powered by <a href="https://hackclub.com" class="underline">Hack Club</a>
    </p>
</footer>
