<script lang="ts">
    import beatlesLyrics from '$lib/beatles_lyrics.json';
    import LineChart from './LineChart.svelte';
    import { stats } from './data';
    const colNum = 5;
</script>

<div class="max-w-4xl mx-auto mt-6 p-2">
    <h1 class="text-center text-2xl">"Love Me Do" to "Goo Goo g'joob"</h1>
    <h2 class="text-center text-xl">The Evolution of Beatles Lyrics</h2>
    <br>
    <div class="flex flex-col items-center">
        <LineChart {stats} />
    </div>
    <!-- <div class="mx-auto text-center w-48 h-56">
        {beatlesLyrics['columns'][colNum]}
        {beatlesLyrics['data'][0][colNum]}
        
    </div> -->
</div>
<div class="h-6"></div>