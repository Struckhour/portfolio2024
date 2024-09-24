<script lang="ts">
    import beatlesLyrics from '$lib/beatles_lyrics.json';
    import LineChart from './LineChart.svelte';
    import { stats } from './data';
    import Menu from '$lib/components/Menu.svelte';

    $: perc = false;
    let yTitle = "Unique Words Per Song"
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

    let wordIndexes: number[] = [1];
    let wordPercs: number[][] = [[]];
    let meanWordPercs: number[] = [];

    function calculateAverage(array: number[]) {
        var total = 0;
        var count = 0;

        array.forEach((item) => {
            total += item;
            count++;
        });

        return total;
    }

    function getMeanSlice(arrayTwoD: number[][], index: number) {
        const slicedArray = arrayTwoD.map((row) => row[index]);
        return calculateAverage(slicedArray);
    }

    $: {
        wordIndexes = [];
        wordPercs = [[]];
        meanWordPercs = [];
        for (let word of wordFilterList) {
            const wordIndex = beatlesLyrics['columns'].findIndex((w) => w === word);
            wordIndexes = [...wordIndexes, wordIndex];   
        }
        wordPercs = wordIndexes.map((wordInd) => beatlesLyrics['data'].map((percArray) => percArray[wordInd]));
        console.log("wordPercs: ", wordPercs)
        for (let i in wordPercs[0]) {
            meanWordPercs.push(getMeanSlice(wordPercs, parseInt(i)))
        }
        if (meanWordPercs.length > 0) {
            perc = true;
            stats.forEach((stat, i) => {
                stats[i].statistic = Number(meanWordPercs[i])
            }) 
        } else {
            stats.forEach((stat, i) => {
                stats[i].statistic = Number(results[i]);
            })
            perc = false;
        }
    }

    $: {
        if (wordIndexes.length > 0) {
            yTitle = "Percentage of Selected Words Out of Total Words"
        } else {
            yTitle = "Unique Words Per Song"
        }
    }

</script>

<div class="max-w-4xl mx-auto mt-6 p-2">
    <h1 class="text-center text-2xl">"Love Me Do" to "Goo Goo G'joob"</h1>
    <h2 class="text-center text-xl">The Evolution of Beatles Lyrics</h2>
    <br>
    <p class="m-auto max-w-3xl mb-4 indent-4">In a few short years, the Beatles went from writing songs about wanting to hold your hand to psychadellics, revolution, and walrus gumboots. As a lifelong Beatles fan, I thought it would be interesting to dive into their lyrics from a data science perspective and see if there might be some thematic and linguistic trends.</p>
    <p class="max-w-3xl indent-4 text-xl m-auto">Choose from some interesting prepared groupings under "Themes" or compare your own custom sets of words under "Words"</p>
    <!-- {albumNames}
    {albumDates} -->

    <Menu bind:filterList={wordFilterList}/>

    {#each wordFilterList as word}
        <button class="rounded-lg bg-blue-300 px-2 py-1 mx-1 hover:bg-blue-200 active:bg-blue-100" on:click={() => {wordFilterList = wordFilterList.filter((w) => w != word)}}>x &nbsp {word}</button>
    {/each}
    <div class="flex flex-col items-center">
        <LineChart stats={stats} title={yTitle} perc={perc} />
    </div>
    <h3 class="text-xl max-w-3xl m-auto">Word Diversity</h3>
    <p class="max-w-3xl m-auto mt-4 indent-4">
        We can see that the Beatles gradually increased in lyrical diversity during the early years, with more unique words per song as time passes. Interestingly, word diversity skyrocketed and peaked in the more experimental/psychadellic albums, Sgt. Peppers and Magical Mystery Tour, and then tapered off again in the later albums. I am reminded of some repetitive and lyrically sparse songs later on such as "I Want You" and "Sun King."
    </p>
    <!-- <div class="mx-auto text-center w-48 h-56">
        {beatlesLyrics['columns'][colNum]}
        {beatlesLyrics['data'][0][colNum]}
        
    </div> -->
    
</div>
<div class="h-6"></div>