<script lang="ts">
    import birdlocs from '$lib/jun22-2023.png';
    import consistency from '$lib/consistency.png';
    import Birdmover from './birdmover.svelte';
</script>

<div class="max-w-3xl mx-auto mt-6 p-2 text-lg">
    <h1 class="text-center text-2xl">Automated Acoustic Triangulation</h1>
    <br>
    <p class="text-center text-2xl text-green-950">Let's play a game!</p>
        <ul class="list-disc text-md">
            <li>Move the bird around in the forest pictured below. </li> 
            <li>Press the 'sing' button and watch how the sound from the bird spreads out and hits each microphone at different times.</li>
            <li>The timeline below the forest shows when the sound hits each microphone.</li>
            <li>See if you can predict where each coloured dot will end up based on where you place the bird.</li>
            <li>Once you're a pro, read on to find out the point of all this!</li>
        </ul>
        
    
    <p class="text-[16px] text-center">
        (I've slowed down the speed of sound dramatically to make it user-friendly)
    </p>

    <hr class="max-w-4xl mx-auto my-6">


    <Birdmover/>

    <div class="text-center tracking-wider w-[90%] max-w-4xl m-auto"><b>Since every position has slightly different timings on the recorders, we can use that data to calculate the bird's position in the forest!</b>
    </div>

    <div class="max-w-4xl mx-auto p-2">
        <br>
        <h2 class="text-lg font-bold">Sounds easy enough, but...</h2>
        <br>
        
        <p>These calculations actually depend on three difficult measurements:    </p>
            <ul class="list-decimal list-inside my-2 ml-2">
                <li><u>GPS:</u> The precise location of each recorder (more precise = better)</li>
                <li><u>Clock Drift:</u> The synchronization of each recorder's imperfect clock </li>
                <li><u>Onset Detection:</u> the precise selection of each song's timing on the different recordings</li>
            </ul> 
            All of these measurements are subject to error, and if we accumulate enough error, our estimated bird locations will be horribly and unpredicatbly wrong!

        <br>
        
        <br>
        <h2 class="text-lg font-bold">Solutions</h2>
        <br>
        
        <p>
            I developed a system and wrote custom Python software to solve each of these problems. If you would like to know more about it, don't hesitate to <a href="https://github.com/Struckhour/triangulation" class="underline" target="_blank">check out the code</a> and/or <a href="/links" target="_blank" class="underline">reach out</a>. The final output includes an image of how two birds (in this case, named 'BBF8' and 'GB1') moved around their territories while singing. Their dots change colour through the rainbow from red to purple as time passes.
        </p>
        <img alt="a graph of birds moving about in the forest while singing." src={birdlocs} />
        <br>
        <h2 class="text-lg font-bold">Results</h2>
        <br>
        <p>
            As of July 2024, I have recorded many birds while they sang and moved about their territories. Now I am analyzing the data. So far the results strongly suggest that neighbouring birds are doing interesting things when they move closer to each other, such as singing faster, interrupting each other, and changing the order of their songs. For example, the graph below shows how one bird orders its songs <i>more predictably</i> as it gets further from its neighbour. Early on in the graph (at the left) it is choosing interesting, unpredictable songs when it is close to its neighbor. Very curious... 
        </p>
        <img alt="a line graph comparing song consistency and distance between birds over time" src={consistency} />
    </div>

    <div class="h-64 max-w-4xl mx-auto"></div>
</div>