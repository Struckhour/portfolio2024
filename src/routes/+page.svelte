    
<script lang='ts'>
    import { goto } from "$app/navigation";
    import forest from '$lib/forest-and-heth.jpg';
    import bulletdrop from '$lib/bulletdrop.png';
    import wordgame from '$lib/wordgame.png';
    import mug from '$lib/mug.png';
    import spec from '$lib/heth_spec_purple.png';
    import beatlepic from '$lib/beatles peppers.png';
    import markovDiagram from '$lib/markov-diagram.png';
    import bird from '$lib/bird.png';
	import { onDestroy, onMount } from "svelte";


    function createCircle(leftPerc: number) {
        const forestBoxDiv = document.getElementById('forestBox');
        if (!forestBoxDiv) {
                return;
            }
        const circle= document.createElement('div');
        circle.style.position = 'absolute';
        circle.style.width = '0%';
        // circle.style.height = `0%`;
        circle.style.aspectRatio = '1/1';
        circle.style.top = `28%`;
        const leftPercentage = 50.5;
        circle.style.left = `${leftPercentage * ((100 - leftPerc * 2)/100) + leftPerc}%`;
        circle.style.border = 'lightblue 10px solid';
        circle.style.opacity = '60%';
        circle.style.borderRadius = '100000px';
        circle.style.transform = 'translate(-50%, -50%)';

        forestBoxDiv.appendChild(circle);
        return circle;
    }

    function createBirdBox(leftPerc: number) {
        const forestBoxDiv = document.getElementById('forestBox');
        if (!forestBoxDiv) {
                return;
            }
        const birdBox= document.createElement('div');
        birdBox.style.position = 'absolute';
        birdBox.style.width = '4%';
        // birdBox.style.height = `0%`;
        birdBox.style.aspectRatio = '1/1';
        birdBox.style.top = `29.8%`;
        const leftPercentage = 49.8;
        birdBox.style.left = `${leftPercentage * ((100 - leftPerc * 2)/100) + leftPerc}%`;
        birdBox.style.border = '#b6ff96 2px dashed';
        birdBox.style.opacity = '60%';
        // birdBox.style.borderRadius = '100000px';
        birdBox.style.transform = 'translate(-50%, -50%)';
        birdBox.style.display = 'none';

        forestBoxDiv.appendChild(birdBox);
        return birdBox;
    }

    const micStats: number[][] = [[25, 4, -45], [25, -6, -138], [25, 0, -80], [5, -7, -110]]

    function createMicDiv(leftPerc: number, micStat: number[]){
        console.log('inside createMidDiv');
        const forestBoxDiv = document.getElementById('forestBox');
        if (!forestBoxDiv) {
                return;
            }
        const micOuterDiv = document.createElement('div');
        forestBoxDiv.appendChild(micOuterDiv);
        micOuterDiv.style.position = 'absolute';
        micOuterDiv.style.width = '100%';
        // micOuterDiv.style.height = '10%'
        micOuterDiv.style.top = `${micStat[0]}%`;
        const leftPercentage = micStat[1];
        micOuterDiv.style.left = `${leftPercentage * ((100 - leftPerc * 2)/100) + leftPerc}%`;
        micOuterDiv.style.transform = `rotate(${micStat[2]}deg)`;
        // micOuterDiv.style.border = 'red 2px solid';
        
        const micDiv= document.createElement('div');
        micDiv.style.width = '0';
        micDiv.style.opacity = '90%';
        micDiv.style.border = '#b6ff96 2px dashed';
        micOuterDiv.appendChild(micDiv);
        return micDiv;
    }

    let songBoxDivs: HTMLDivElement[] = [];
    let songBoxLocs = [[1, 40, 3, 40],
                     [7, 60, 3, 25],
                     [12.8, 52, 3, 30],
                     [19, 6, 3, 50],
                     [24.8, 24, 3, 50],
                     [31.5, 56, 3, 25],
                     [37.5, 60, 3, 25],
                     [44, 6, 3, 50],
                     [50, 56, 3, 25],
                     [55.5, 49, 3, 30],
                     [63.5, 55, 3, 25],
                     [68.5, 24, 3, 50],
                     [75.5, 49, 3, 30],
                     [79.5, 3, 3, 50],
                     [85.5, 49, 3, 40],
                     [93.5, 36, 3, 50],

                    ]
// Function to handle div creation 
    function createScanLine(leftPerc: number) {
        const specBoxDiv = document.getElementById('specBox');
        if (!specBoxDiv) {
                return;
            }


        const scanLine= document.createElement('div');
        scanLine.style.position = 'absolute';
        scanLine.style.width = '0px';
        scanLine.style.height = `100%`;
        scanLine.style.top = `0%`;
        scanLine.style.left = `${leftPerc}%`;
        scanLine.style.border = 'lightblue 2px solid';
        scanLine.style.opacity = '60%';
        specBoxDiv.appendChild(scanLine);
        return scanLine;
    }

    function createSongBox(leftPerc: number, locArray: number[]) {
        const specBoxDiv = document.getElementById('specBox');
        if (!specBoxDiv) {
                return;
            }
        const songBox = document.createElement('div');
        songBoxDivs.push(songBox)
        songBox.style.position = 'absolute';
        songBox.style.width = `${locArray[2]}%`;
        songBox.style.height = `${locArray[3]}%`;
        songBox.style.top = `${locArray[1]}%`;
        songBox.style.left = `${locArray[0] * ((100 - leftPerc * 2)/100) + leftPerc}%`;
        songBox.style.border = 'lightblue 2px solid';
        songBox.style.opacity = '80%';
        specBoxDiv.appendChild(songBox);
    };

    let specInterval: ReturnType<typeof setInterval>;
    let scanLine: HTMLDivElement | undefined;

    let forestInterval: ReturnType<typeof setInterval>;
    let birdCircle: HTMLDivElement | undefined;
    let micDivA: HTMLDivElement | undefined;
    let micDivB: HTMLDivElement | undefined;
    let micDivC: HTMLDivElement | undefined;
    let micDivD: HTMLDivElement | undefined;
    let birdBox: HTMLDivElement | undefined;

    onDestroy(() => {
        clearInterval(specInterval);
    })

    function restartForest() {
        clearInterval(forestInterval);
        if (birdCircle) birdCircle.remove();
    	const forestDiv = document.getElementById('forestDiv');
        if (!forestDiv) {
                return;
            }
        const forestLoc = forestDiv.offsetLeft
        const forestWidth = forestDiv.offsetWidth;
        if (micDivA) micDivA.remove();
        if (micDivB) micDivB.remove();
        if (micDivC) micDivC.remove();
        if (micDivD) micDivD.remove();
        if (birdBox) birdBox.remove();
        const totalWidth = forestLoc + forestLoc + forestWidth;
        const leftPerc = forestLoc/totalWidth * 100;
        const rightEdge = 100 - leftPerc;
        let circleSize = 0;
        const biggestCircle = 250;
        let micAWidth = 0;
        let micBWidth = 0;
        let micCWidth = 0;
        let micDWidth = 0;
        birdCircle = createCircle(leftPerc);
        micDivA = createMicDiv(leftPerc, micStats[0]);
        micDivB = createMicDiv(leftPerc, micStats[1]);
        micDivC = createMicDiv(leftPerc, micStats[2]);
        micDivD = createMicDiv(leftPerc, micStats[3]);
        birdBox = createBirdBox(leftPerc);
        forestInterval = setInterval(() => {
            if (birdCircle) {
                if (circleSize < biggestCircle) {
                    circleSize += 1;
                    birdCircle.style.width = `${circleSize}%`;

                    // birdCircle.style.height = `${circleSize}%`;
                } else {
                    circleSize = 0;
                    micAWidth = 0;
                    if(micDivA) micDivA.style.width = `${micAWidth}%`;
                    micBWidth = 0;
                    if(micDivB) micDivB.style.width = `${micBWidth}%`;
                    micCWidth = 0;
                    if(micDivC) micDivC.style.width = `${micCWidth}%`;
                    micDWidth = 0;
                    if(micDivD) micDivD.style.width = `${micDWidth}%`;
                    if(birdBox) birdBox.style.display = 'none';
                }
                if (circleSize > 90) {
                    if (micAWidth < 42) micAWidth += 1;
                    if (micDivA) micDivA.style.width = `${micAWidth}%`;
                }
                if (circleSize > 90) {
                    if (micBWidth < 42) micBWidth += 1;
                    if (micDivB) micDivB.style.width = `${micBWidth}%`;
                }
                if (circleSize > 100) {
                    if (micCWidth < 44) micCWidth += 1;
                    if (micDivC) micDivC.style.width = `${micCWidth}%`;
                }
                if (circleSize > 65) {
                    if (micDWidth < 28) micDWidth += .5;
                    if (micDivD) micDivD.style.width = `${micDWidth}%`;
                }
                if (circleSize > 150) {
                    if (birdBox) birdBox.style.display = 'block';
                }
            }
        }, 15) 
    }

    function restartSpec() {
        clearInterval(specInterval);
        songBoxDivs.forEach((div) => div.remove());
        if (scanLine) scanLine.remove();
    	const specDiv = document.getElementById('specDiv');
        if (!specDiv) {
                return;
            }
        const specLoc = specDiv.offsetLeft
        const specWidth = specDiv.offsetWidth;
        console.log("specLoc: ", specLoc)
        console.log("specWidth: ", specWidth);
        const totalWidth = specLoc + specLoc + specWidth;
        const leftPerc = specLoc/totalWidth * 100;
        const rightEdge = 100 - leftPerc
        let lineLoc = leftPerc;
        
        scanLine = createScanLine(leftPerc);
        let songIndex = 0;
        let allDone = false;
        specInterval = setInterval(() => {
            if (scanLine) {
                if (lineLoc < rightEdge) {
                    lineLoc += .2;
                    if (lineLoc > (songBoxLocs[songIndex][0] * ((100 - leftPerc * 2)/100) + leftPerc) && !allDone) {
                        createSongBox(leftPerc, songBoxLocs[songIndex]);
                        if (songIndex < songBoxLocs.length -1) {songIndex++;}
                        else {allDone = true;}
                    }
                } else {
                    lineLoc = leftPerc;
                    songIndex = 0;
                    allDone = false;
                    songBoxDivs.forEach((div) => div.remove());
                }
                scanLine.style.left = `${lineLoc}%`  
            }
        }, 15) 
    }

    onMount(()=>{
        window.addEventListener('resize', onResize);
        restartSpec();
        restartForest();
        return () => window.removeEventListener('resize', onResize);
    });

    function onResize() {
        restartSpec();
        restartForest();
    }



</script>

<svelte:window />
<!-- <div class="mt-8 mb-2 mx-auto max-w-4xl">
    <h1 class="text-3xl text-center text-green-950">Luke McLean</h1>
    <h2 class="text-center text-slate-600">problem solver, researcher, software developer, educator</h2>
</div> -->

<!-- <div class="mt-12 max-w-2xl mx-auto text-lg" style="background-image: url({forest})">

</div> -->

<!-- triangulation -->
<div class="relative bg-black">
    <div id="forestBox" class="relative bg-black overflow-hidden max-w-6xl m-auto">

        <div class="absolute w-full text-5xl z-40 text-white bottom-4 lg:bottom-12 rounded-2xl bg-black bg-opacity-50 px-4 py-2">
            <div class="text-left ml-[5%] text-xl md:text-2xl lg:text-5xl">
                Automated Acoustic Triangulation
            </div>
        </div>
        <!-- <div class="border border-green-500 top-[29.8%] left-[49.8%] w-12 aspect-square absolute z-50"></div> -->
        <img id="forestDiv" alt="a forest" src={forest} class="relative mx-auto w-full max-w-6xl object-scale-down"/>
    </div>
</div>

<div class="text-center text-2xl mt-4 mb-12">
    <p class="max-w-2xl mx-auto my-2">

        For my master's research, I developed an automated system for tracking birds while they sing in the forest. I was able to demonstrate that neighbouring hermit thrushes interact through movement and song.
    </p>
    <button on:click={() => goto("/triangulation")} class="border-2 border-green-900 rounded-full px-4 bg-green-900 bg-opacity-20 hover:bg-opacity-60 transition-opacity hover:text-white text-lg sm:text-2xl">
        Learn more
    </button>
</div>

<!-- HethFinder -->

<div id="specBox" class="relative bg-black">

    <div class="absolute text-5xl z-40 text-white bottom-4 lg:bottom-12 bg-black rounded-2xl px-4 py-2 bg-opacity-50 w-full">
        <div class="text-right mr-[10%] text-xl md:text-2xl lg:text-5xl">
            Birdsong Detector with Machine Learning
        </div>
    </div>
    <img id="specDiv" alt="a dense forest" src={spec} class="relative mx-auto w-full max-w-6xl object-scale-down"/>
</div>


<div class="text-center text-2xl mt-4 mb-8">
    <p class="max-w-xl mx-auto my-2">
        During my time at the University of New Brunswick, I wrote software that would detect and categorize hermit thrush vocalizations on recordings. The program uses machine learning and spectrogram analysis with Python and TensorFlow.
    </p>
    <button on:click={() => goto("/hethfinder")} class="border-2 border-green-900 rounded-full px-4 bg-green-900 bg-opacity-20 hover:bg-opacity-60 transition-opacity hover:text-white text-lg sm:text-2xl">
        Learn more
    </button>
</div>

<!-- Bulletdrop Compendium -->

<div class="relative">

    <div class="absolute text-5xl z-40 w-full text-white bottom-4 lg:bottom-12 bg-black rounded-2xl px-4 py-2 bg-opacity-50">
        <div class="text-left ml-[10%] text-xl md:text-2xl lg:text-5xl">
            The Ghost Recon Bulletdrop Compendium
        </div>
    </div>
    <img alt="a dense forest" src={bulletdrop} class="relative w-full max-h-[600px] object-cover"/>
</div>


<div class="text-center text-2xl mt-4 mb-8">
    <p class="max-w-xl mx-auto my-2">
        I was hired to design and create this site that displays the bulletdrop for various rifles and scopes in the ghost recon video game series.
    </p>
    <button on:click={() => goto("/ghost")} class="border-2 border-green-900 rounded-full px-4 bg-green-900 bg-opacity-20 hover:bg-opacity-60 transition-opacity hover:text-white text-lg sm:text-2xl">
        Learn more
    </button>
    <a href="https://bulletdrop.netlify.app" target="_blank" class="border-2 border-green-900 rounded-full px-4 bg-green-900 bg-opacity-20 hover:bg-opacity-60 transition-opacity hover:text-white text-lg sm:text-2xl">Check out the site</a>
</div>

<!-- Beatles -->

<div class="relative opacity-90">

    <div class="absolute text-5xl z-40 text-white bottom-4 lg:bottom-12 w-full bg-black rounded-2xl px-4 py-2 bg-opacity-50">
        <div class="text-right mr-[15%] text-xl md:text-2xl lg:text-5xl">
            Beatles Lyrics Over Time
        </div>
    </div>
    <img alt="a dense forest" src={beatlepic} class="relative w-full max-h-[600px] object-cover object-top"/>
</div>

<div class="text-center text-2xl mt-4 mb-8">
    <p class="max-w-xl mx-auto my-2">
        Recently, out of curiosity, I built an interactive dashboard for exploring how beatles' lyrics changed over time.
    </p>
    <button on:click={() => goto("/beatles")} class="border-2 border-green-900 rounded-full px-4 bg-green-900 bg-opacity-20 hover:bg-opacity-60 transition-opacity hover:text-white text-lg sm:text-2xl">
        Check it out
    </button>
</div>

<!-- Markov -->

<div class="relative bg-black">

    <div class="absolute text-5xl z-40 text-white bottom-4 lg:bottom-12 w-full bg-black rounded-2xl px-4 py-2 bg-opacity-50">
        <div class="text-left ml-[10%] text-xl md:text-2xl lg:text-5xl">
            Markov Chains in Animal Communication
        </div>
    </div>
    <img alt="a dense forest" src={markovDiagram} class="relative w-full max-h-[600px] object-contain"/>
    <img alt="a bird singing" src={bird} class="absolute w-24 opacity-80 aspect-square left-[49%] top-2/4 -translate-x-2/4 -translate-y-2/4"/>

</div>

<div class="h-48 text-center text-2xl mt-4 mb-8">
    <p class="max-w-xl mx-auto my-2">
        For my honours research, I used computer simulations to explore how a hermit thrush orders its songs, like words being arranged into long, complex sentences.
    </p>
    <button on:click={() => goto("/markov")} class="border-2 border-green-900 rounded-full px-4 bg-green-900 bg-opacity-20 hover:bg-opacity-60 transition-opacity hover:text-white text-lg sm:text-2xl">
        Learn more
    </button>
</div>


<!-- Ent-tris -->

<div class="relative bg-gradient-to-r from-transparent to-green-950 to-30%">

    <!-- <div class="absolute text-5xl z-40 text-white bottom-12 right-[15%] bg-black rounded-2xl px-4 py-2 bg-opacity-50">Ent-tris</div> -->
    <img alt="a dense forest" src={wordgame} class="relative w-full m-auto max-w-xl max-h-[600px] object-cover"/>
</div>

<div class="h-48 text-center text-2xl">
    <p class="max-w-xl mx-auto my-2">
        A word-building game I made for fun. It combines Tetris with Scrabble and knowledge of JRR Tolkien's The Lord of the Rings.
    </p>
    <a href="https://ent-ris.vercel.app" target="_blank" class="border-2 border-green-900 rounded-full px-4 bg-green-900 bg-opacity-20 hover:bg-opacity-60 transition-opacity hover:text-white text-lg sm:text-2xl">Check out the site</a>
</div>

<!-- Pottery -->

<div class="relative bg-slate-200">

    <!-- <div class="absolute text-5xl z-40 text-white bottom-12 left-[15%] bg-black rounded-2xl px-4 py-2 bg-opacity-50"></div> -->
    <img alt="a dense forest" src={mug} class="relative w-full max-w-2xl mx-auto max-h-[600px] object-cover aspect-square rounded-full"/>
</div>

<div class="h-48 text-center text-2xl">
    <p class="max-w-xl mx-auto my-2">
        An artist website I made for a local potter.
    </p>
    <a href="https://katherinemccordpottery.com" target="_blank" class="border-2 border-green-900 rounded-full px-4 bg-green-900 bg-opacity-20 hover:bg-opacity-60 transition-opacity hover:text-white text-lg sm:text-2xl">Check out the site</a>
</div>



    

