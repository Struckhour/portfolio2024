<script lang="ts">
    import beatlesLyrics from '$lib/beatles_lyrics.json';
    import LineChart from './LineChart.svelte';
    const colNum = 5;
</script>

<div class="max-w-2xl mx-auto mt-6 p-2 text-xl text-left">
    <h1 class="text-center text-2xl">The Evolution of Beatles Lyrics</h1>
    <br>
    <div class="mx-auto text-center w-48 h-56">
        {beatlesLyrics['columns'][colNum]}
        {beatlesLyrics['data'][0][colNum]}
        
    </div>
    <p class="mt-4">
        A few years ago, HeavyHawk, an avid player of Ghost Recon:Breakpoint (the popular video game) hired me to build a <a href="https://bulletdrop.netlify.app" target="_blank" class="underline">website</a> that could tell players how much their <a href="https://en.wikipedia.org/wiki/External_ballistics" target="_blank" class="underline">bullets would drop as they move through the air.</a> This is no simple question because:
        <ol class="mt-2 list-decimal ml-6">
            <li>the game does not obey real-world physics. </li>
            <li>the rifles and attachments do not behave as stated in-game. </li>
            <li>the bullet behavior is different for all the different combinations of rifles, attachments, and scopes.</li>
        </ol>
        
        <br>   
        <p>
        HeavyHawk tested <i>many</i> individual rifle combinations and we built <a href="https://bulletdrop.netlify.app" target="_blank" class="underline">this free site</a> so that keen gamers can finally hit (very) long-range shots with all their favourite loadouts. The website is designed to be quick and easy to use (just select a rifle and a scope and read the mildots), but there is actually a ton of information if one wants to dig around and nerd out on the fictional physics and statistics.
    </p>
</div>
<div class="h-6"></div>