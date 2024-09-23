<script lang="ts">
    import beatlesLyrics from '$lib/beatles_lyrics.json';
    import LineChart from './LineChart.svelte';
    import { stats } from './data';
    import Menu from '$lib/components/Menu.svelte';



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
    stats.forEach((stat, i) => {
        stats[i].statistic = Number(results[i])
    }) 
    let wordFilterList: string[] = [];
</script>

<div class="max-w-4xl mx-auto mt-6 p-2">
    <h1 class="text-center text-2xl">"Love Me Do" to "Goo Goo G'joob"</h1>
    <h2 class="text-center text-xl">The Evolution of Beatles Lyrics</h2>
    <br>
    
    <p>In a few short years, the Beatles went from writing songs about wanting to hold your hand to psychadellics, revolution, and walrus gumboots. As a lifelong Beatles fan, I thought it would be interesting to dive into lyrics from a data science perspective and see if there might be thematic and linguistic trends.</p>
    <!-- {albumNames}
    {albumDates} -->
    <Menu bind:filterList={wordFilterList}/>
    {#each wordFilterList as word}
        <button class="rounded-lg bg-blue-300 px-2 py-1 mx-1 hover:bg-blue-200 active:bg-blue-100" on:click={() => {wordFilterList = wordFilterList.filter((w) => w != word)}}>x &nbsp {word}</button>
    {/each}
    <div class="flex flex-col items-center">
        <LineChart {stats} />
    </div>
    <p class="max-w-3xl m-auto mt-4">
        First, we can see that the Beatles gradually increased in lyrical complexity during the early years, with more unique words per song as time passes. Interestingly, this skyrocketed and peaked in the more psychadellic albums, Sgt. Peppers and Magical Mystery Tour, and then tapered off again in the later albums. I am reminded of some lyrically sparse songs in the last year such as "I Want You" and "Sun King."
    </p>
    <!-- <div class="mx-auto text-center w-48 h-56">
        {beatlesLyrics['columns'][colNum]}
        {beatlesLyrics['data'][0][colNum]}
        
    </div> -->
    
</div>
<div class="h-6"></div>