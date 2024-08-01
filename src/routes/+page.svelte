    
<script>
    import { goto } from "$app/navigation";
</script>

<div class="mt-12 mx-auto max-w-4xl">
    <h1 class="text-3xl text-center text-green-950">Luke McLean</h1>
    <h2 class="text-center text-slate-600">problem solver, researcher, software developer, educator</h2>
    <!-- <hr class="block border-t border-slate-300"> -->
</div>


<div class="max-w-2xl mx-auto mt-6 text-lg">
    <p class="my-4 text-center">

        Hello! I put this site together to share some of the science research, software, and web development projects that I have worked on in the past few years. Enjoy!
    </p>
    <p class="text-center text-base">
        (If you'd like to contact me: lukecmclean@gmail.com)
    </p>
</div>

<hr class="border-t border-green-900 max-w-4xl my-4 mx-auto">

<div class="grid grid-cols-[40%_20%_40%] grid-rows-5 max-w-4xl mx-auto gap-y-8">

    <h1 class="text-center text-2xl mt-6">
        Research and Data Analysis
    </h1>
    <div></div>
    <h1 class="text-center text-2xl mt-6">
        Web Development
    </h1>

    <button on:click={() => goto("projects/triangulation")} class="border border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40">
        Automated Acoustic Triangulation of Animal Locations
    </button>
    <div class="flex justify-center items-center">
        <div class="h-8 text-lg font-bold">--2024--</div>
    </div>
    <button on:click={() => goto("projects/wordgame")} class="border border-slate-300 hover:border-blue-900 hover:border-2 rounded-full bg-blue-800 bg-opacity-30 hover:bg-opacity-40">
        A fun little word game
    </button>

    <button on:click={() => goto("projects/hethfinder")} class="border-2 border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40">
        Detecting and Classifying Sounds with Machine Learning
    </button>
    <div class="flex justify-center items-center">
        <div class="h-8 text-lg font-bold">--2023--</div>
    </div>    
    <button on:click={() => goto("projects/ghost")} class="border border-slate-300 hover:border-blue-900 hover:border-2 rounded-full px-4 bg-blue-800 bg-opacity-30 hover:bg-opacity-40">
        The Ghost Recon Bulletdrop Compendium
    </button>
    
    
    <button on:click={() => goto("projects/markov")} class="border border-slate-300 hover:border-green-900 hover:border-2 rounded-full px-4 bg-green-800 bg-opacity-30 hover:bg-opacity-40">
        Markov Chains in Animal Communication!
    </button>

    <div class="flex justify-center items-center">
        <div class="h-8 text-lg font-bold">--2020-2022--</div>
    </div>  

    <button on:click={() => goto("projects/pottery")} class="border border-slate-300 hover:border-blue-900 hover:border-2 rounded-full px-4 bg-blue-800 bg-opacity-30 hover:bg-opacity-40">
        A Local Artist's Website
    </button>


</div>
    

