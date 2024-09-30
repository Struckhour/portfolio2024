    
<script>
    import { goto } from "$app/navigation";
    import forest from '$lib/forest.jpg';
    import bulletdrop from '$lib/bulletdrop.png';
    import wordgame from '$lib/wordgame.png';
    import mug from '$lib/mug.png';
</script>

<!-- <div class="mt-8 mb-2 mx-auto max-w-4xl">
    <h1 class="text-3xl text-center text-green-950">Luke McLean</h1>
    <h2 class="text-center text-slate-600">problem solver, researcher, software developer, educator</h2>
</div> -->

<!-- <div class="mt-12 max-w-2xl mx-auto text-lg" style="background-image: url({forest})">

</div> -->

<!-- triangulation -->
<div class="relative opacity-90 hover:opacity-100 hover:cursor-pointer">

    <div class="absolute text-5xl z-40 text-white bottom-12 left-[15%] bg-black rounded-2xl px-4 py-2 bg-opacity-50">Automated Acoustic Triangulation</div>
    <img alt="a dense forest" src={forest} class="relative w-full max-h-[600px] object-cover"/>
</div>

<div class="text-center text-2xl mt-4 mb-12">
    <p class="max-w-xl mx-auto my-2">

        For my master's research, I developed an automated system for tracking birds while they sing in the forest.
    </p>
    <button on:click={() => goto("/triangulation")} class="border-2 border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-lg sm:text-2xl">
        Learn more
    </button>
</div>

<!-- HethFinder -->

<div class="relative opacity-90 hover:opacity-100 hover:cursor-pointer">

    <div class="absolute text-5xl z-40 text-white bottom-12 right-[15%] bg-black rounded-2xl px-4 py-2 bg-opacity-50">Birdsong Detector with Machine Learning</div>
    <img alt="a dense forest" src={forest} class="relative w-full max-h-[600px] object-cover"/>
</div>


<div class="text-center text-2xl mt-4 mb-8">
    <p class="max-w-xl mx-auto my-2">
        During my time at the University of New Brunswick, I wrote software that would detect and categorize hermit thrush vocalizations on recordings. This used machine learning and spectrogram analysis with Python and TensorFlow.
    </p>
    <button on:click={() => goto("/hethfinder")} class="border-2 border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-lg sm:text-2xl">
        Learn more
    </button>
</div>

<!-- Bulletdrop Compendium -->

<div class="relative opacity-90 hover:opacity-100 hover:cursor-pointer">

    <div class="absolute text-5xl z-40 text-white bottom-12 left-[15%] bg-black rounded-2xl px-4 py-2 bg-opacity-50">The Ghost Recon Bulletdrop Compendium</div>
    <img alt="a dense forest" src={bulletdrop} class="relative w-full max-h-[600px] object-cover"/>
</div>


<div class="text-center text-2xl mt-4 mb-8">
    <p class="max-w-xl mx-auto my-2">
        I was hired to design and create this site that displays the bulletdrop for various rifles and scopes in the ghost recon video game series.
    </p>
    <button on:click={() => goto("/ghost")} class="border-2 border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-lg sm:text-2xl">
        Learn more
    </button>
    <a href="https://bulletdrop.netlify.app" target="_blank" class="border-2 border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-lg sm:text-2xl">Check out the site</a>
</div>

<!-- Beatles -->

<div class="relative opacity-90 hover:opacity-100 hover:cursor-pointer">

    <div class="absolute text-5xl z-40 text-white bottom-12 right-[15%] bg-black rounded-2xl px-4 py-2 bg-opacity-50">Beatles Lyrics Over Time</div>
    <img alt="a dense forest" src={forest} class="relative w-full max-h-[600px] object-cover"/>
</div>

<div class="h-48 text-center text-2xl">
    <p class="max-w-xl mx-auto my-2">
        Recently, for fun and out of curiosity, I built an interactive dashboard for checking how beatles' lyrics changed over time.
    </p>
    <button on:click={() => goto("/beatles")} class="border border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-xl sm:text-2xl">
        Learn more
    </button>
</div>

<!-- Markov -->

<div class="relative opacity-90 hover:opacity-100 hover:cursor-pointer">

    <div class="absolute text-5xl z-40 text-white bottom-12 left-[15%] bg-black rounded-2xl px-4 py-2 bg-opacity-50">Markov Chains in Animal Communication!</div>
    <img alt="a dense forest" src={forest} class="relative w-full max-h-[600px] object-cover"/>
</div>

<div class="h-48 text-center text-2xl">
    <p class="max-w-xl mx-auto my-2">
        For my honours research, I used computer simulations to explore how a hermit thrush orders its songs, like words being arranged into long, complex sentences.
    </p>
    <button on:click={() => goto("/markov")} class="border border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-xl sm:text-2xl">
        Learn more
    </button>
</div>


<!-- Ent-tris -->

<div class="relative opacity-90 hover:opacity-100 hover:cursor-pointer bg-green-950">

    <!-- <div class="absolute text-5xl z-40 text-white bottom-12 right-[15%] bg-black rounded-2xl px-4 py-2 bg-opacity-50">Ent-tris</div> -->
    <img alt="a dense forest" src={wordgame} class="relative w-full m-auto max-w-xl max-h-[600px] object-cover"/>
</div>

<div class="h-48 text-center text-2xl">
    <p class="max-w-xl mx-auto my-2">
        This is a word-building game I made for fun. It combines Tetris with Scrabble and knowledge of JRR Tolkien's The Lord of the Rings.
    </p>
    <a href="https://ent-ris.vercel.app" target="_blank" class="border-2 border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-lg sm:text-2xl">Check out the site</a>
</div>

<!-- Pottery -->

<div class="relative opacity-90 hover:opacity-100 hover:cursor-pointer bg-black">

    <div class="absolute text-5xl z-40 text-white bottom-12 left-[15%] bg-black rounded-2xl px-4 py-2 bg-opacity-50"></div>
    <img alt="a dense forest" src={mug} class="relative w-full max-w-2xl mx-auto max-h-[600px] object-cover rounded-full"/>
</div>

<div class="h-48 text-center text-2xl">
    <p class="max-w-xl mx-auto my-2">
        This is an artist website I made for a local potter.
    </p>
    <a href="https://katherinemccordpottery.com" target="_blank" class="border-2 border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-lg sm:text-2xl">Check out the site</a>
</div>



    

