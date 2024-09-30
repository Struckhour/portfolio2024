    
<script>
    import { goto } from "$app/navigation";
    import forest from '$lib/forest.jpg';
</script>

<!-- <div class="mt-8 mb-2 mx-auto max-w-4xl">
    <h1 class="text-3xl text-center text-green-950">Luke McLean</h1>
    <h2 class="text-center text-slate-600">problem solver, researcher, software developer, educator</h2>
</div> -->

<!-- <div class="mt-12 max-w-2xl mx-auto text-lg" style="background-image: url({forest})">

</div> -->

<img alt="a dense forest" src={forest} class="w-full max-h-[600px] object-cover"/>



<div class="grid grid-cols-2 grid-rows-5 max-w-4xl mx-auto px-1 gap-y-8 gap-x-4">
    <h1 class="text-center text-2xl mt-6">
        Research and Data Analysis
    </h1>
    <h1 class="text-center text-2xl mt-6">
        Web Development
    </h1>

    <button on:click={() => goto("/triangulation")} class="border border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-sm sm:text-lg">
        Automated Acoustic Triangulation
    </button>

    <button on:click={() => goto("/wordgame")} class="border border-slate-300 hover:border-blue-900 hover:border-2 rounded-full bg-blue-800 bg-opacity-30 hover:bg-opacity-40 text-sm sm:text-lg">
        A fun little word game
    </button>

    <button on:click={() => goto("/beatles")} class="border border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-sm sm:text-lg">
        Beatles Lyrics Analyzer
    </button>
    
    <button on:click={() => goto("/ghost")} class="border border-slate-300 hover:border-blue-900 hover:border-2 rounded-full px-4 bg-blue-800 bg-opacity-30 hover:bg-opacity-40 text-sm sm:text-lg">
        The Ghost Recon Bulletdrop Compendium
    </button>

    <button on:click={() => goto("/hethfinder")} class="border-2 border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-sm sm:text-lg">
        ML Birdsong Classifier
    </button>
    
    <button on:click={() => goto("/pottery")} class="border border-slate-300 hover:border-blue-900 hover:border-2 rounded-full px-4 bg-blue-800 bg-opacity-30 hover:bg-opacity-40 text-sm sm:text-lg">
        A Local Artist's Website
    </button>
    
    <button on:click={() => goto("/markov")} class="border border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40 text-sm sm:text-lg">
        Markov Chains in Animal Communication!
    </button>



    <div>
    </div>
</div>
    

