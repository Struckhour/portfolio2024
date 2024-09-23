<script lang="ts">
    import beatlesLyrics from '$lib/beatles_lyrics.json';
    import LineChart from './LineChart.svelte';
    import { stats } from './data';
    const colNum = 5;
    const albumNames = beatlesLyrics['data'].map((data) => {
        return data[0]
    });
    const albumDates = beatlesLyrics['data'].map((data) => {
        return data[1]
    })
    const results = beatlesLyrics['data'].map((data) => {
        return data[4]
    })
    for (let i in stats) {
        stats[parseInt(i)].statistic = results[i]
    }
</script>

<div class="max-w-4xl mx-auto mt-6 p-2">
    <h1 class="text-center text-2xl">"Love Me Do" to "Goo Goo G'joob"</h1>
    <h2 class="text-center text-xl">The Evolution of Beatles Lyrics</h2>
    <br>
    <p>People of the 1960s witnessed a rapid transformation in popular music, exemplified and partly driven by the music of The Beatles. In a few short years, they went from writing songs about wanting to hold your hand to psychadellic imagery to world peace and walrus gumboots. As a lifelong Beatles fan, I thought it would be interesting to dive into the lyrics from their twelve studio albums and see if there might be insights that shed light on these transformative years.</p>
    <!-- {albumNames}
    {albumDates} -->
    <div class="flex flex-col items-center">
        <LineChart {stats} />
    </div>
    <!-- <div class="mx-auto text-center w-48 h-56">
        {beatlesLyrics['columns'][colNum]}
        {beatlesLyrics['data'][0][colNum]}
        
    </div> -->
</div>
<div class="h-6"></div>