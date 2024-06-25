<script lang="ts">
    import hermit from '$lib/Hermit_thrush_qmnonic.jpg';
	import { fade } from 'svelte/transition';
    import Birdmover from './birdmover.svelte';
    let showText = true;


</script>

<div class="max-w-2xl mx-auto mt-6 p-2 text-xl">
    <h1 class="text-center text-2xl">Automated Acoustic Triangulation of Animal Locations</h1>
    <br>
    For my master's research (2022-2024), I am exploring how birds move about their territories as they sing, especially in relation to their closest neighbours.
    There are few studies that have tracked movement for long periods of natural singing between neighbours, and none with my study species, the hermit thrush. Consequently, the research has involved innovation, extensive problem solving, and custom software development to track moment-to-moment bird positions with our lab's automated recorders.
    <br>

</div>
<div class="h-6"></div>
<hr class="max-w-4xl mx-auto">
<div class="h-6"></div>

<button type="button" on:click={() => (showText = !showText)} class="block max-w-2xl mx-auto mt-4 p-2 text-xl underline text-center rounded-lg">
    
    <div class={showText?"text-slate-500":"text-black"}>{showText?'Read less' : 'Read more'}</div>
</button>
{#if showText}
<div transition:fade class="max-w-4xl mx-auto p-2">
    <br>
    <p>The idea of triangulating a sound source is old and relatively simple, but the implementation can be very complicated. To get a sense of the math, move the singing bird around in the forest picture below. Watch how the timing of its song hitting each recorder changes based on where it is in the forest. Each location in the forest has a unique set of timings across the recorders!
    </p>
    <br>

    <Birdmover/>
    <div class="text-center tracking-wider w-[90%] m-auto"><b>What this means is that if we know the timing of a given song on each recorder, we can calculate the bird's position in the forest!</b>
    </div>
    
    <br>
    <h2 class="text-lg font-bold">So, why is it difficult?</h2>
    <br>
    
    <p>Each measurement of song timing actually depends on three measurements:    </p>
        <ul class="list-decimal list-inside my-2 ml-2">
            <li><u>GPS:</u> The location of each recorder</li>
            <li><u>Clock Drift:</u> The synchronization of each recorder's clock </li>
            <li><u>Onset Detection:</u> the precise selection of each song's timing on the different recorders</li>
        </ul> 
        All of these measurements are subject to error, and if we accumulate enough error, our estimated bird locations will be horribly and unpredicatbly wrong!

    <br>
    
    <br>
    <h2 class="text-lg font-bold">Solutions</h2>
    <br>
    
    <p>
        I wrote <a href="https://github.com/Struckhour" class="underline" target="_blank">custom software</a> to solve each of these problems, but in order to keep things brief here, I'll focus on the most interesting one: detecting the onset of each song on each recorder.
    </p>
    <br>
    <h2 class="text-lg font-bold">Results</h2>
    <br>
    <p>
        As of July 2024, I am analyzing the data. I have recorded all the birds and calculated their moment-to-moment locations, and am now making the statistical comparisons that check whether two neighbours' change their singing based on their movements and location. So far the results are promising. The graph below shows how one bird's song order (syntax) relates to distance from its neighbour. More specifically, the bird orders its songs less predictably as it gets closer to its neighbour! I wonder what that's all about! 
    </p>
</div>
{/if}
<div class="h-64"></div>