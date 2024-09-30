<script lang="ts">
    import notes1 from '$lib/Slide1.jpg';
    import notes2 from '$lib/Slide2.jpg';
    import hermit from '$lib/Hermit_thrush_qmnonic.jpg';
</script>

<div class="h-20 w-full"></div>
<div class="max-w-2xl mx-auto mt-6 p-2 text-xl text-center">
    <h1 class="text-center text-2xl">Markov Analysis of Birdsong</h1>
    <br>
    For my honours research in 2020, I explored how birds order their songs into complex sequences.
    This involved generating thousands of computer simulations of song sequences and comparing those simulations to real bird recordings. 
    <br>
    The research was published in the
     <a href="https://link.springer.com/article/10.1007/s10336-020-01840-2" target="_blank" class="underline">Journal of Ornithology</a>,
      but a less academic summary can be read below and
      the R code for generating simulated sequences can be found on my <a href="https://github.com/Struckhour/markov" target="_blank" class="underline">github page</a>.
</div>
<div class="h-6"></div>
<hr class="max-w-4xl mx-auto">
<div class="h-6"></div>

<img alt="a hermit thrush." src={hermit} class="w-48 h-48 m-auto rounded-full object-cover"/>

<div class="max-w-4xl mx-auto p-2">
    <br>
    <p>A hermit thrush (seen above) is a forest-dwelling bird known for its beautiful, haunting song. However, what most people hear and think of as a singular repeating
    2-second song is actually slightly different versions being ordered into complex sequences (like words being ordered into sentences).
    It cycles through its 10-15 song-types and chooses the next one based on what it has previously sung.
    For example, it almost never sings the same song-type twice in a row.
    The question I set out to answer was quite simple:
    </p>
    <br>
    <div class="text-center tracking-wider w-[90%] m-auto"><b>How many previous songs influence the upcoming song choice? In other words, how much does a bird care what it recently sang?</b>
    </div>
    
    <br>
    <h2 class="text-lg font-bold">First Method</h2>
    <br>
    
    <p>One way to explore this questions is to ask: if I know the most recent song, does that help me predict what the next song will be? 
        What if I know the most recent two songs? Three songs, etc.?
    </p>
    <br>
    <p>First, I recorded <b><i>a lot</i></b> of hermit thrush song. After selecting and identifying the thousands of individual songs (with help from lab-mates), 
        I looked at the transitions from one song to the next and and asked if the upcoming song differs depending on what was recently sung.
        For example, maybe every time a bird sings song D it follows with either song G or song C. </p>
    <br>
    <img alt="song transitioning from D to either C or G" src={notes1}/>
        <p>So, how does it decide between the two options, G or C?
        If we look a little closer, we see that nearly every time the bird sings song A before song D, it follows with song G. 
        But, when it sings song F before song D, it follows with song C.</p>
    <img alt="songs transitioning predictably once previous songs are known." src={notes2}/>
        <p>
        So, in this case, we need to know two previous songs in order to make a good prediction of what the next song will be.
        It is not enough that we know the most recent song.
        But what if we go further back? Perhaps the bird is even <i>more</i> likely to follow up with G after song D if D is preceded by J, B, and then A. 
        Is there a limit to how much predictive power we gain by looking further back in the sequence?
        I looked at all the most common transitions up to four songs back and used Fisher's Tests to measure whether there is a statistical difference between the sequences.
    </p>
    
    <br>
    <h2 class="text-lg font-bold">Second Method</h2>
    <br>
    
    <p>
        The other thing we can do is measure the proportion of song G or C that followed song D. 
        We can then generate a thousand simulations of singing bouts that use those measured proportions to choose the next song.
        Every time the computer produces a song D in the sequence, it chooses the next song, G or C, based on the proportions of G and C that followed D in the actual recording.
        We can then compare the simulated sequences to actual sequences of song: if the simulations are similar to the birds real singing, then the bird must be using similar rules when choosing its songs.
    </p>
    <br>
    <h2 class="text-lg font-bold">Results</h2>
    <br>
    <p>
        I was able to collect enough song recordings of fourteen different birds to measure whether it was useful to know the previous four songs.
        And it was! This suggests that a bird remembers what it sang about 20 seconds ago and uses that knowledge to decide what to sing next.
        However, I found that knowing <i>two</i> previous songs provided the largest gains in predictive accuracy. 
        Knowing three and four previous songs offered diminishing returns. This suggests that the bird is much more concerned with its most recent singing.
        Why? What are they saying? Who are they singing to? That is what I am exploring in my <a href="triangulation" class="underline">master's research</a>!
    </p>
</div>
<div class="h-64 max-w-2xl"></div>

