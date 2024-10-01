<script lang="ts">
    import beatlesLyrics from '$lib/beatles_lyrics.json';
    import LineChart from './LineChart.svelte';
    import { stats } from './data';
    import Menu from '$lib/components/Menu.svelte';
    import ThemeMenu from '$lib/components/ThemeMenu.svelte';
    import { themes } from '$lib/themes';

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
            yTitle = "Percentage of Selected Words Out of an Album's Total Words"
        } else {
            yTitle = "Unique Words Per Song"
        }
    }

    $: {
        wordFilterList = themes[theme];
    }

    let theme = 'Word Diversity (None)';
</script>


<div class="h-20 w-full"></div>
<div class="max-w-4xl mx-auto mt-6 p-2">
    <h1 class="text-center text-2xl text-white py-2 bg-gradient-to-r from-transparent via-slate-700 to-transparent">"Love Me Do" to "Goo Goo G'joob"</h1>
    <h2 class="text-center text-xl text-white py-2 bg-gradient-to-r from-transparent via-slate-700 to-transparent">The Evolution of Beatles Lyrics</h2>
    <br>
    <p class="m-auto max-w-xl mb-4 indent-4">In a few short years, the Beatles went from writing songs about wanting to hold your hand to psychedelics, revolution, and walrus gumboots. Explore these changes in the interactive graph below.</p>
    <p class="max-w-3xl indent-4 text-xl m-auto">Choose from prepared groupings under "Themes" or compare your own custom sets of words under "Words." Let me know if you find any interesting word combinations and I'll add them to the themes list!</p>
    <!-- {albumNames}
    {albumDates} -->
    <div class="w-full flex mt-4 mb-2 justify-evenly">
        <ThemeMenu bind:selectedTheme={theme}/>
        <Menu bind:filterList={wordFilterList}/>
    </div>
    <div>

        {#each wordFilterList as word}
        <button class="rounded-lg bg-blue-300 px-2 py-1 mx-1 my-1 hover:bg-blue-200 active:bg-blue-100" on:click={() => {wordFilterList = wordFilterList.filter((w) => w != word)}}>x &nbsp {word}</button>
        {/each}
    </div>
    <div class="flex flex-col items-center">
        <LineChart stats={stats} title={yTitle} perc={perc} />
    </div>


    {#if (wordFilterList.length == 0)}
    <h3 class="text-xl max-w-3xl m-auto">Word Diversity</h3>
    <p class="max-w-3xl m-auto mt-4 indent-4">
        We can see that the Beatles gradually increased in lyrical diversity during the early years, with more unique words per song as time passes. Interestingly, word diversity skyrocketed and peaked in the more experimental/psychedelic albums, Sgt. Peppers and Magical Mystery Tour, and then tapered off again in the later albums. I am reminded of some repetitive and lyrically sparse songs later on such as "I Want You" and "Sun King."
    </p>
    {/if}
    {#if theme == 'Positivity' && (wordFilterList.length > 0)}
    <h3 class="text-xl max-w-3xl m-auto">Positivity</h3>
    <p class="max-w-3xl m-auto mt-4 indent-4">
        Here we can see a general avoidance of overtly positive words such as 'good' and 'great,' <i>except</i> for a marked increase starting in the mid-60s as they begin to experiment with drugs and novel sounds and approaches in the studio. Sgt. Pepper's is often thought of as their most groundbreaking, creative, contribution to popular music. Lyrically, it also seems to be their happiest contribution.
    </p>
    {/if}
    {#if theme == 'Negativity' && (wordFilterList.length > 0)}
    <h3 class="text-xl max-w-3xl m-auto">Negativity</h3>
    <p class="max-w-3xl m-auto mt-4 indent-4">
        Somewhat consistent with the positivity graph, we can see that around the same time they increased their usage of positive words, they also reduced their usage of negative words such as 'bad,' 'worse,' and 'sad.'
    </p>
    {/if}
    {#if theme == 'Ego' && (wordFilterList.length > 0)}
    <h3 class="text-xl max-w-3xl m-auto">Ego</h3>
    <p class="max-w-3xl m-auto mt-4 indent-4">
        As they embraced psychedelic drugs and Eastern philosophies, their usage of words that refer to one's self decreased dramatically (about 6x less!). It then increased again as some band members passed through this cultural/philosophical phase and they wrote their final two albums, "Let it Be" and "Abbey Road."
    </p>
    {/if}
    {#if theme == 'Oneness' && (wordFilterList.length > 0)}
    <h3 class="text-xl max-w-3xl m-auto">Oneness</h3>
    <p class="max-w-3xl m-auto mt-4 indent-4">
        On the flip side of the Ego chart, their usage of words relating to 'oneness' and 'togetherness' increased during the same years that references to 'self' decreased.
    </p>
    {/if}
    {#if theme == 'Masculine' && (wordFilterList.length > 0)}
    <h3 class="text-xl max-w-3xl m-auto">Masculinity</h3>
    <p class="max-w-3xl m-auto mt-4 indent-4">
        I was curious to see whether their might be gender changes over the years, such as an increase or decrease in references to men. Overall, references to men did not change much (note the Y-axis only accounts for about 2%), but references to women or feminine terms had a more interesting trend (see 'Feminine').
    </p>
    {/if}
    {#if theme == 'Feminine' && (wordFilterList.length > 0)}
    <h3 class="text-xl max-w-3xl m-auto">Femininity</h3>
    <p class="max-w-3xl m-auto mt-4 indent-4">
        Unlike with masculine terms, their usage of feminine terms saw significant changes over the years, with a major focus on women/girls in the first half of their career (except A Hard Days Night) and a major drop off as they became more experimental and lyrically diverse. Similar to references to the 'self', we see a little uptick in the last two albums.
    </p>
    {/if}
    {#if theme == 'Travel' && (wordFilterList.length > 0)}
    <h3 class="text-xl max-w-3xl m-auto">Travel</h3>
    <p class="max-w-3xl m-auto mt-4 indent-4">
        There is a small, general, increase in travel-related words over time, possibly just a result of increasing lyrical diversity. I mostly included this graph to provide an example of the type of custom categories one could explore.
    </p>
    {/if}
    <!-- <div class="mx-auto text-center w-48 h-56">
        {beatlesLyrics['columns'][colNum]}
        {beatlesLyrics['data'][0][colNum]}
        
    </div> -->
    
</div>
<div class="h-24"></div>