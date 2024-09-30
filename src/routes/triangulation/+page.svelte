<script lang="ts">
    import birdlocs from '$lib/jun22-2023.png';
    import consistency from '$lib/consistency.png';
    import Birdmover from './birdmover.svelte';
	import Youtube from '$lib/components/Youtube.svelte';
    import heat_map from '$lib/conventional_heat_map.png';
</script>

<div class="h-20 w-full"></div>
<div class="max-w-5xl mx-auto p-2 text-lg">
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

    <div class="max-w-6xl mx-auto p-2">
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
        <h2 class="text-2xl text-center">Results</h2>
        <br>
        
        <p class="indent-4 mb-4">
            I developed a system and wrote custom Python software to solve each of these problems. If you would like to know more about it, don't hesitate to <a href="https://github.com/Struckhour/triangulation" class="underline" target="_blank">check out the code</a> and/or <a href="/links" target="_blank" class="underline">reach out</a>. The final output can be used to generate a video animation of the birds' singing:
        </p>
        <Youtube />
        <h2 class="text-lg font-bold mt-4">Overlap</h2>
        <p class="indent-4">
            This is only a small segment of a 50-minute countersinging bout. Nonetheless, if observed carefully, it demonstrates how the bird in the bottom left (blue) sings more often than its neighbour and frequently interrupts, whereas the bird in the top right (orange) generally avoids interrupting. Though this portion of the bout does not show much movement, these birds also statistically sang more quickly when nearer to each other. Such overlapping dynamics and changes in song rate were observed across many of the birds and 'neighbourhoods' recorded.
        </p>

        <h2 class="text-lg font-bold mt-2">Conventional Matching</h2>
        <p class="indent-4">
            Most impressively, birds also responded to each other's specific song-types disproportionately, preferring to respond to certain song-types with their own favoured responses. This is known as 'conventional matching' because birds are responding by arbitrary convention rather than by matching some acoustic property, such as similar pitch or song structure. The heat map (below) demonstrates how the focal bird preferentially responded with song 'A' and song 'L' to its neighbour's song 'D'.
        </p>
        <img class="mt-2 text-center m-auto" alt="a heat map of a birds favoured responses to its neighbour's songs." src={heat_map} />
        <p class="indent-4 mt-2">

            Such preferential responses require a bird to learn its neighbour's repertoire. What they are signaling with such responses remains unclear, but it could be an unmistakable way to demonstrate familiarity and attention ("I know you, I know your songs, and I am listening"). It could also be a much more complicated interaction.
    </p>
        <p class="indent-4 mt-8">
            The software can also generate an image of how two birds moved around their territories while singing. Their dots change colour through the rainbow from red to purple as time passes.
        </p>
        <img class="mt-2" alt="a graph of birds moving about in the forest while singing." src={birdlocs} />
        <br>
        <h2 class="text-lg font-bold">Summary</h2>
        <br>
        <p class="indent-4">
            I recorded 19 birds in 2023 and 2024, for about an hour each, while they sang and moved about their territories. Overall, the results strongly suggest that neighbouring birds are interacting through song and movement. In addition to the above findings, the data showed differences in overlapping rates, singing rates, song-switch rates, and frequency matching rates when birds were near to each other versus far apart. This research also provided the first documented case of two hermit thrushes sharing song-types, and it explored a new type of countersinging in which birds burst into a rapid flurry of soft singing followed by a long period of silence.
        </p>
        <!-- <img alt="a line graph comparing song consistency and distance between birds over time" src={consistency} /> -->
    </div>

    <div class="h-64 max-w-4xl mx-auto"></div>
    
</div>