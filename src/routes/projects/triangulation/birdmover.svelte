<script lang="ts">
    import microphone from '$lib/microphone.jpg';
    import birdPic from '$lib/bird.png';
    import {onMount,onDestroy} from "svelte";
    import trees from '$lib/trees.jpg';
    
    // let counter = 0;
    let interval: number;
    let clockInterval: number;
    let latestBirdX = 25;
    let latestBirdY = 25;
    const micPositions: {[mic: string]: {[dimension: string]: number}} = {
        A: {x: 50, y: 15}, 'B': {x: 85, y: 50}, 'C': {x: 50, y: 50}, 'D': {x: 25, y: 75}
    }

    let currentOrigin = {x: latestBirdX, y: latestBirdY}
    let litA = false;
    let litB = false;
    let litC = false;
    let litD = false;
    let timeA = '';
    let timeB = '';
    let timeC = '';
    let timeD = '';
    
    function formatTime(date: Date) {
        const hh = date.getHours() % 12;
        let mm = date.getMinutes().toString();
        let ss = date.getSeconds().toString();
        const ml = date.getMilliseconds().toString()
        if (mm.length < 2) {
            mm = '0' + mm;
        }
        if (ss.length < 2) {
            ss = '0' + ss;
        }
        return `${hh}:${mm}:${ss}.${ml[0]}`
    }

    function resetMics() {
        timeA = '';
        timeB = '';
        timeC = '';
        timeD = '';
    }

    function resetInterval()
    {
        resetMics();
        litA = false;
        litB = false;
        litC = false;
        litD = false;
        let soundCircle = document.getElementById('soundCircle');
            if (!soundCircle) {
                return;
            }
        soundCircle.style.left = `${latestBirdX}%`;
        soundCircle.style.top = `${latestBirdY}%`;
        currentOrigin = {x: latestBirdX, y: latestBirdY};

    	clearInterval(interval);
    	interval = setInterval(()=>{
            let soundCircle = document.getElementById('soundCircle');
            if (!soundCircle) {
                lastTweet = 100;
                return;
            }
            if (Date.now() - lastFrame > 30) {
                pingWidth += 2;
                pingHeight += 2;
                soundCircle.style.width = `${pingWidth}%`;
                soundCircle.style.height = `${pingHeight}%`;

                const distToA = getDistance(micPositions.A, currentOrigin);
                const distToB = getDistance(micPositions.B, currentOrigin);
                const distToC = getDistance(micPositions.C, currentOrigin);
                const distToD = getDistance(micPositions.D, currentOrigin);

                if ((distToA < pingWidth / 2) && !litA) {
                    litA = true;
                    timeA = formatTime(new Date())
                }
                if (distToB < pingWidth / 2 && !litB) {
                    litB = true;
                    timeB = formatTime(new Date());
                }
                if (distToC < pingWidth / 2 && !litC) {
                    litC = true;
                    timeC = formatTime(new Date())
                }
                if (distToD < pingWidth / 2 && !litD) {
                    litD = true;
                    timeD = formatTime(new Date())
                }
                
                lastFrame = Date.now();
                //reset ping
                if (litA && litB && litC && litD) {
                    pingWidth = 0;
                    pingHeight = 0;
                    soundCircle.style.width = `${pingWidth}%`;
                    soundCircle.style.height = `${pingHeight}%`;
                }
            }        

    	}, 10)
    }
    
    onMount(()=>{
    	resetClock();
    });
    
    onDestroy(()=>{
    	clearInterval(interval);
        clearInterval(clockInterval);
    });
    
    function resetClock() {
        clockInterval = setInterval(() => {
        currentTimestamp = formatTime(new Date());
        }, 10)
    }
    let now = new Date();
    // get the current date and time as a string
    let currentTimestamp = formatTime(now);

    let inBox = false;

    let lastTweet = 0;
    let pingWidth = 20;
    let pingHeight = 20;
    let lastFrame = 0;
    
    const timeInterval = setInterval(() => {

    }, 1000)


    let birdGrabbed = false;

    let m = { x: 0, y: 0 };
    function moveBird(event: MouseEvent) {
        if (!birdGrabbed) return;
        let boxCoords = getMouseOnBox(event, 'forest');
        if (boxCoords === undefined) return;
        if (boxCoords.x > 100 || boxCoords.x < 0 || boxCoords.y > 100 || boxCoords.y < 0) {
            inBox = false;
        } else {
            inBox = true;
        }
        

        if (!inBox) {
            // replaceBirdPosition()
            return;
        }
        updateBirdPosition(boxCoords.x, boxCoords.y);
    }

    function getMouseOnBox(event: MouseEvent, id: string) {
        let box = document.getElementById(id)
        if (!box) {
            return;
        }
        let boxData = box.getBoundingClientRect();
        m.x = event.clientX;
        m.y = event.clientY;
        let boxX = m.x - boxData.x;
        let boxY = m.y - boxData.y;
        let xPerc = boxX / boxData.width * 100;
        let yPerc = boxY / boxData.height * 100;
        return {x: xPerc, y: yPerc};
    }



    function updateBirdPosition(x: number, y: number) {
        let bird = document.getElementById("bird");
        let birdVeil = document.getElementById("birdVeil");
        if (!bird) return;
        if (!birdVeil) return;
        latestBirdX = x;
        latestBirdY = y;
        birdVeil.style.left = `${x}%`;
        birdVeil.style.top = `${y}%`;
        bird.style.left = `${x}%`;
        bird.style.top = `${y}%`;
    }
    function replaceBirdPosition() {
        let bird = document.getElementById("bird");
        if (!bird) return;
        bird.style.left = `25%`;
        bird.style.top = `25%`;
    }


    function getDistance(micPos: Record<string, number>, soundOrigin: {x: number, y: number}) {
        const dist = ((soundOrigin.x - micPos.x)**2 + (soundOrigin.y - micPos.y)**2)**.5
        return dist;
    }
    function handleClick() {
        resetInterval();
    }
    let instruct = true;

</script>

<button on:click={handleClick} class="block mx-auto border border-slate-500 text-xl rounded-xl p-2 m-1 bg-slate-200 z-50">Sing</button>
<div on:mousemove={moveBird} role="alert" id="forest" class="relative w-[30rem] h-[30rem] mx-auto mb-4">
    <img id="trees" alt="some sketched trees" src={trees} class="object-cover w-[30rem] h-[30rem] opacity-50 pointer-events-none">
    <!-- bird -->
    <img id="bird" alt="a bird" src={birdPic} class="absolute w-[20%] h-[20%] top-1/4 left-1/4 -translate-y-2/4 -translate-x-2/4 z-20 cursor-pointer pointer-events-none"/>
    <div id="birdVeil" on:mousedown={() => {birdGrabbed = true; instruct = false}} on:mouseup={() => birdGrabbed = false} class="absolute w-[20%] h-[20%] top-1/4 left-1/4 -translate-y-2/4 -translate-x-2/4 z-30 cursor-pointer"></div>
    <!-- sound circle -->
    <div id="soundCircle" class="absolute border border-black rounded-full top-1/4 z-10 -translate-y-2/4 left-1/4 -translate-x-2/4"></div>

    <!-- microphones -->
    <img id="micA" alt="microphone A" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-2/4 top-[15%] -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute z-0 left-2/4 top-[8%] -translate-y-2/4 -translate-x-2/4 bg-white">{timeA}</div>
    {#if litA}
    <div class="absolute border-2 border-red-500 rounded-full w-[10%] h-[10%] left-2/4 top-[15%] -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}
    <img id="micB" alt="microphone B" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-[85%] top-2/4  -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute z-0 left-[85%] top-[42%] -translate-y-2/4 -translate-x-2/4 bg-white">{timeB}</div>
    {#if litB}
    <div class="absolute border-2 border-green-500 rounded-full w-[10%] h-[10%] left-[85%] top-2/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}
    <img id="micC" alt="microphone C" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-2/4 top-2/4 -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute z-0 left-2/4 top-[42%] -translate-y-2/4 -translate-x-2/4 bg-white">{timeC}</div>
    {#if litC}
    <div class="absolute border-2 border-blue-500 rounded-full w-[10%] h-[10%] left-2/4 top-2/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}
    <img id="micD" alt="microphone D" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-1/4 top-3/4 -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute z-0 left-1/4 top-[65%] -translate-y-2/4 -translate-x-2/4 bg-white">{timeD}</div>
    {#if litD}
    <div class="absolute border-2 border-purple-500 rounded-full w-[10%] h-[10%] left-1/4 top-3/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}
    {#if instruct}
    <div class="absolute w-[40%] h-[20%] top-[2%] left-[-10px] -translate-y-2/4 -translate-x-2/4 z-20 cursor-pointer pointer-events-none">Drag bird to move around!</div>
    {/if}
    <div class="absolute top-[93%] w-24 left-2/4 -translate-x-2/4 px-2 py-1 bg-white text-xl z-50">
        <div>{currentTimestamp}</div>
    </div>
</div>
