<script lang="ts">
import Navigation from '$lib/components/Navigation.svelte';
import Section from '$lib/components/Section.svelte';
import IdeaItem from '$lib/components/IdeaItem.svelte';
import PrizeCard from '$lib/components/PrizeCard.svelte';
import Button from '$lib/components/Button.svelte';

import { onMount } from 'svelte';

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
        href: 'https://wizardzines.com/zines/terminal',
        alt: 'The Secrets Rules of the Terminal'
    },
    {
        href: 'https://wizardzines.com/zines/bite-size-command-line',
        alt: 'Bite Size Command Line!'
    },
    {
        href: 'https://wizardzines.com/zines/bite-size-linux',
        alt: 'Bite Size Linux!'
    },
    {
        href: 'https://wizardzines.com/zines/bite-size-bash',
        alt: 'Bite Size Bash!'
    },
    {
        href: 'https://wizardzines.com/zines/bite-size-networking',
        alt: 'Bite Size Networking!'
    },
    {
        href: 'https://wizardzines.com/zines/git',
        alt: 'How Git Works'
    },
    {
        href: 'https://wizardzines.com/zines/integers-floats',
        src: 'https://wizardzines.com/zines/integers-floats/cover.png',
        alt: 'How Integers and Floats Work'
    },
    {
        href: 'https://wizardzines.com/zines/debugging-guide',
        alt: 'The Pocket Guide to Debugging'
    },
    {
        href: 'https://wizardzines.com/zines/dns',
        alt: 'How DNS Works'
    },
    {
        href: 'https://wizardzines.com/zines/css',
        src: 'https://wizardzines.com/zines/css/cover.png',
        alt: 'Hell Yes! CSS!'
    },
    {
        href: 'https://wizardzines.com/zines/containers',
        alt: 'How Containers Work!'
    },
    {
        href: 'https://wizardzines.com/zines/sql',
        alt: 'Become a SELECT star!'
    },
    {
        href: 'https://wizardzines.com/zines/http',
        alt: 'HTTP: Learn your browser\'s language!'
    },
    {
        href: 'https://wizardzines.com/zines/oh-shit-git',
        alt: 'Oh shit, git!'
    },
    {
        href: 'https://wizardzines.com/zines/manager',
        alt: 'Help! I have a manager!'
    }
];

let scrollContainer :Element;
let isHovered = false;

onMount(() => {
    let scrollAmount = 0;
    const step = 1;
    const delay = 6;

    const scroll = () => {
        if (scrollContainer && !isHovered) {
            scrollAmount += step;
            if (scrollAmount >= scrollContainer.scrollWidth - scrollContainer.clientWidth) {
                scrollAmount = 0;
            }
            scrollContainer.scrollLeft = scrollAmount;
        }
    };

    const interval = setInterval(scroll, delay);

    const handleMouseEnter = () => { isHovered = true; };
    const handleMouseLeave = () => { isHovered = false; };

    if (scrollContainer) {
        scrollContainer.addEventListener('mouseenter', handleMouseEnter);
        scrollContainer.addEventListener('mouseleave', handleMouseLeave);
    }

    return () => {
        clearInterval(interval);
        if (scrollContainer) {
            scrollContainer.removeEventListener('mouseenter', handleMouseEnter);
            scrollContainer.removeEventListener('mouseleave', handleMouseLeave);
        }
    };
});
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
        and we'll reward your wisdom with a zine by <a href="https://wizardzines.com" target="_blank" class="text-yellow-800 underline">Julia Evans</a>.
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
    <div bind:this={scrollContainer} class="overflow-x-auto whitespace-nowrap scrollbar-hide">
        {#each prizes as prize}
        <PrizeCard href={prize.href} src={prize.src ?? ''} alt={prize.alt} />
        {/each}
    </div>
    <!--<p class="mt-6 text-gray-700 italic">You will get all of them! <i>(depend on the ysws scale)</i></p>-->
</Section>

<style>
    .scrollbar-hide {
        -ms-overflow-style: none;  /* Internet Explorer 10+ */
        scrollbar-width: none;  /* Firefox */
    }
    .scrollbar-hide::-webkit-scrollbar { 
        display: none;  /* Safari and Chrome */
    }
</style>

<!-- RSVP Section -->
<section id="rsvp" class="bg-[#f3ede0] py-20 px-6 text-center pt-14 pb-14">
    <h3 class="text-2xl font-semibold text-yellow-900">Here's the rules you must follow </h3>
    <ul class="list-disc text-left inline-block mx-auto mt-4 pb-8">
        <li>Track more than 2 hours with <a class="text-yellow-800 underline" href="https://hackatime.hackclub.com/">Hackatime</a></li>
        <li title="Two Hackclubbers can't do a tutorial on the same subject.">Be original within the ysws</li>
        <li title="Spellcheck/translation allowed">No AI should be used to generate content</li>
        <li>Tutorial must be publicly accessible for everyone forever</li>
        <li>Credit any sources you used</li>
        <li>Be 18 or younger</li>
    </ul>

    <h2 class="text-3xl font-semibold text-yellow-900 mb-6">Ready to share?</h2>
    <p class="text-lg mb-4 text-gray-800">Submit your tutorial and get your zine.</p>
    <Button href="https://forms.hackclub.com/home">RSVP Now</Button>
</section>

<!-- Footer -->
<footer class="bg-[#f9f6ec] py-6 text-center text-sm text-gray-600 border-t border-gray-300">
    <p>Made with love and scrolls by @<a href="https://github.com/MathiasDPX" class="underline">mathias</a> 📚</p>
    <p>
        Source on <a href="https://github.com/MathiasDPX/glossarium" class="underline">GitHub</a> • Powered by <a href="https://hackclub.com" class="underline">Hack Club</a>
    </p>
</footer>