<script lang="ts">
    import microphone from '$lib/microphone.jpg';
    import birdPic from '$lib/bird.png';
    import {onMount,onDestroy} from "svelte"
    
    // let counter = 0;
    let interval: number;
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

    
    function resetInterval()
    {
    	clearInterval(interval);
    	interval = setInterval(()=>{
            now = new Date();
            const hh = now.getHours();
            const mm = now.getMinutes();
            const ss = now.getSeconds();
            const ml = now.getMilliseconds().toFixed(1)
            if (inBox) currentTimestamp = `${hh}:${mm}:${ss}.${ml[0]}`;

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

                if (distToA < pingWidth / 2) {
                    litA = true;
                }
                if (distToB < pingWidth / 2) {
                    litB = true;
                }
                if (distToC < pingWidth / 2) {
                    litC = true;
                }
                if (distToD < pingWidth / 2) {
                    litD = true;
                }
                
                lastFrame = Date.now();

                if (pingWidth >  220) {
                    soundCircle.style.left = `${latestBirdX}%`;
                    soundCircle.style.top = `${latestBirdY}%`;
                    currentOrigin = {x: latestBirdX, y: latestBirdY};
                    pingWidth = 1;
                    pingHeight = 1;
                    litA = false;
                    litB = false;
                    litC = false;
                    litD = false;
                }
            }        

    	}, 10)
    }
    
    onMount(()=>{
    	resetInterval();
    });
    
    onDestroy(()=>{
    	clearInterval(interval);
    });
    

    let now = new Date();
    // get the current date and time as a string
    let currentTimestamp = now.toLocaleString();

    let inBox = false;

    let lastTweet = 0;
    let pingWidth = 20;
    let pingHeight = 20;
    let lastFrame = 0;
    
    const timeInterval = setInterval(() => {

    }, 1000)




    let m = { x: 0, y: 0 };
    function handleMousemove(event: MouseEvent) {
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
        if (!bird) return;
        latestBirdX = x;
        latestBirdY = y;
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

</script>

<div role="alert" id="forest" on:mousemove={handleMousemove} class="relative border border-green-600 w-96 h-96 mx-auto cursor-none">
    <!-- bird -->
    <img id="bird" alt="a bird" src={birdPic} class="absolute w-[20%] h-[20%] top-1/4 left-1/4 -translate-y-2/4 -translate-x-2/4 z-20"/>
    <!-- sound circle -->
    <div id="soundCircle" class="absolute border border-black rounded-full top-1/4 z-10 -translate-y-2/4 left-1/4 -translate-x-2/4"></div>

    <!-- microphones -->
    <img id="micA" alt="microphone A" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-2/4 top-[15%] -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute h-[10%] z-0 left-2/4 top-[10%] -translate-y-2/4 -translate-x-2/4">Mic A: </div>
    {#if litA}
    <div class="absolute border-2 border-red-500 rounded-full w-[10%] h-[10%] left-2/4 top-[15%] -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}
    <img id="micB" alt="microphone B" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-[85%] top-2/4  -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute h-[10%] z-0 left-[85%] top-[45%] -translate-y-2/4 -translate-x-2/4">Mic B: </div>
    {#if litB}
    <div class="absolute border-2 border-green-500 rounded-full w-[10%] h-[10%] left-[85%] top-2/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}
    <img id="micC" alt="microphone C" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-2/4 top-2/4 -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute h-[10%] z-0 left-2/4 top-[45%] -translate-y-2/4 -translate-x-2/4">Mic C: </div>
    {#if litC}
    <div class="absolute border-2 border-blue-500 rounded-full w-[10%] h-[10%] left-2/4 top-2/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}
    <img id="micD" alt="microphone D" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-1/4 top-3/4 -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute h-[10%] z-0 left-1/4 top-[70%] -translate-y-2/4 -translate-x-2/4">Mic D: </div>
    {#if litD}
    <div class="absolute border-2 border-purple-500 rounded-full w-[10%] h-[10%] left-1/4 top-3/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}
</div>
<div class="w-96 mx-auto mb-4">
    <div>Time: {currentTimestamp}</div>
</div>