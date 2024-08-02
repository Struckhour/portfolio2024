<script lang="ts">
    import microphone from '$lib/microphone.jpg';
    import birdPic from '$lib/bird.png';
    import {onMount,onDestroy} from "svelte";
    import trees from '$lib/trees.jpg';
    import highsong from '$lib/highsong.wav';
    import lowsong from '$lib/lowsong.wav';
    import mute from '$lib/mute.png';
    import muteoff from '$lib/muteoff.svg';

    let audioContext: AudioContext;
    let audioBuffer: AudioBuffer | null = null;
    let sourceNode: AudioBufferSourceNode | null = null;

  // Function to load the audio file
    const loadAudio = async (url: string) => {
        const response = await fetch(url);
        const arrayBuffer = await response.arrayBuffer();
        audioBuffer = await audioContext.decodeAudioData(arrayBuffer);
        playAudio();
    };

    // Function to play the audio
    const playAudio = () => {
        if (audioBuffer) {
        sourceNode = audioContext.createBufferSource();
        sourceNode.buffer = audioBuffer;
        sourceNode.connect(audioContext.destination);
        sourceNode.start(0);
        }
    };

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
    let timeAms = 0;
    let timeBms = 0;
    let timeCms = 0;
    let timeDms = 0;
    
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

    function turnOffDot(id: string) {
        let dot = document.getElementById(id);
        if (!dot) {
            return;
        }
        dot.style.opacity = '0%';
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
        const songTime = Date.now();
        for (let dot of ['redbox', 'greenbox', 'bluebox', 'purplebox']) {
            turnOffDot(dot);
        }

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
                    timeAms = Date.now();
                    timeA = formatTime(new Date());
                    let redBox = document.getElementById('redbox');
                    if (!redBox) {
                        return;
                    }
                    redBox.style.left = `${((timeAms - songTime) / (4000))*100}%`;
                    redBox.style.opacity = '70%';
                }
                if (distToB < pingWidth / 2 && !litB) {
                    litB = true;
                    timeBms = Date.now()
                    timeB = formatTime(new Date());
                    let greenBox = document.getElementById('greenbox');
                    if (!greenBox) {
                        return;
                    }
                    greenBox.style.left = `${((timeBms - songTime) / (4000))*100}%`;
                    greenBox.style.opacity = '70%';
                }
                if (distToC < pingWidth / 2 && !litC) {
                    litC = true;
                    timeCms = Date.now();
                    timeC = formatTime(new Date());
                    let blueBox = document.getElementById('bluebox');
                    if (!blueBox) {
                        return;
                    }
                    blueBox.style.left = `${((timeCms - songTime) / (4000))*100}%`;
                    blueBox.style.opacity = '70%';
                }
                if (distToD < pingWidth / 2 && !litD) {
                    litD = true;
                    timeDms = Date.now();
                    timeD = formatTime(new Date());
                    let purpleBox = document.getElementById('purplebox');
                    if (!purpleBox) {
                        return;
                    }
                    purpleBox.style.left = `${((timeDms - songTime) / (4000))*100}%`;
                    purpleBox.style.opacity = '70%';
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
    
    let birdVeil: HTMLElement|null = document.getElementById('birdVeil')
    let isDragging = false;
    let offsetX = 0;
    let offsetY = 0;
    let bird: HTMLElement|null = document.getElementById('bird');
    let forest: HTMLElement|null = document.getElementById('forest')

    function onTouchStart(event: TouchEvent) {
    isDragging = true;
    const touch = event.touches[0];
    if (birdVeil) {
        offsetX = touch.clientX - birdVeil.offsetLeft;
        offsetY = touch.clientY - birdVeil.offsetTop;
    }
  }

  function onTouchMove(event: TouchEvent) {
    if (isDragging) {
      const touch = event.touches[0];
      if (birdVeil && bird) {
          birdVeil.style.left = `${touch.clientX - offsetX}px`;
          birdVeil.style.top = `${touch.clientY - offsetY}px`;
          bird.style.left = `${touch.clientX - offsetX}px`;
          bird.style.top = `${touch.clientY - offsetY}px`;
      }
    }
  }

  function onTouchEnd() {
    isDragging = false;
  }

    onMount(()=>{
    	resetClock();
        if (birdVeil) birdVeil.addEventListener("touchstart", onTouchStart);
        if (forest) {
            forest.addEventListener("touchmove", onTouchMove);
            forest.addEventListener("touchend", onTouchEnd);
        }
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
    let birdGrabbed = false;
    let instruct = true;

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

    function getDistance(micPos: Record<string, number>, soundOrigin: {x: number, y: number}) {
        const dist = ((soundOrigin.x - micPos.x)**2 + (soundOrigin.y - micPos.y)**2)**.5
        return dist;
    }
    let muted = false;
    let highlow = true;
    function handleClick() {
        resetInterval();
        if (!muted) {
            audioContext = new AudioContext();
            if (highlow) {loadAudio(highsong)} else {loadAudio(lowsong)};
            highlow = !highlow;
            playAudio;
        }
    }

    function muteButton() {
        muted = !muted;
    }
</script>
<div class="relative left-2/4 -translate-x-2/4">
    <button on:click={handleClick} class="relative left-2/4 -translate-x-2/4 border border-slate-500 text-xl rounded-xl p-2 m-1 bg-slate-200 z-40 hover:bg-slate-300 active:bg-slate-100">Sing</button>
    {#if !muted}
    <button on:click={muteButton} class="absolute bottom-2 left-3/4 border-2 border-slate-500 rounded-xl p-2 bg-slate-50 z-40 hover:bg-slate-300 active:bg-slate-100 w-10 h-10">
        <img alt="volume icon" src={muteoff} class = "w-full h-full"/>
    </button>
    {:else}
    <button on:click={muteButton} class="absolute bottom-2 left-3/4 border border-black rounded-xl p-2 bg-slate-200 z-40 hover:bg-slate-300 active:bg-slate-100 w-10 h-10">
        <img alt="mute icon" src={mute} class = "w-full h-full"/>
    </button>
    {/if}
</div>

<div on:mousemove={moveBird} role="alert" id="forest" class="relative w-screen aspect-square sm:aspect-auto sm:w-[30rem] sm:h-[30rem] mx-auto border border-green-700">
    <img id="trees" alt="some sketched trees" src={trees} class="object-cover w-screen aspect-square sm:aspect-auto sm:w-[30rem] sm:h-[30rem] opacity-50 pointer-events-none">
    <!-- bird -->
    <img id="bird" alt="a bird" src={birdPic} class="absolute w-[20%] h-[20%] top-1/4 left-1/4 -translate-y-2/4 -translate-x-2/4 z-20 cursor-pointer pointer-events-none"/>
    <!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
    <div id="birdVeil" role="alert" on:mousedown={() => {birdGrabbed = true; instruct = false}} on:mouseup={() => birdGrabbed = false} class="absolute w-[20%] h-[20%] top-1/4 left-1/4 -translate-y-2/4 -translate-x-2/4 z-30 cursor-pointer"></div>
    <!-- sound circle -->
    <div id="soundCircle" class="absolute border border-black rounded-full top-1/4 z-10 -translate-y-2/4 left-1/4 -translate-x-2/4"></div>

    <!-- microphones -->
    <img id="micA" alt="microphone A" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-2/4 top-[15%] -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute z-0 left-2/4 top-[8%] -translate-y-2/4 -translate-x-2/4 bg-white">{timeA}</div>
    {#if litA}
    <div class="absolute border-4 border-orange-500 opacity-70 rounded-full w-[10%] h-[10%] left-2/4 top-[15%] -translate-y-2/4 -translate-x-2/4"> </div>
    {:else}
    <div class="absolute border border-orange-500 opacity-70 rounded-full w-[10%] h-[10%] left-2/4 top-[15%] -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}

    <img id="micB" alt="microphone B" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-[85%] top-2/4  -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute z-0 left-[85%] top-[42%] -translate-y-2/4 -translate-x-2/4 bg-white">{timeB}</div>
    {#if litB}
    <div class="absolute border-4 border-green-500 opacity-70 rounded-full w-[10%] h-[10%] left-[85%] top-2/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {:else}
    <div class="absolute border border-green-500 opacity-70 rounded-full w-[10%] h-[10%] left-[85%] top-2/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}
    
    <img id="micC" alt="microphone C" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-2/4 top-2/4 -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute z-0 left-2/4 top-[42%] -translate-y-2/4 -translate-x-2/4 bg-white">{timeC}</div>
    {#if litC}
    <div class="absolute border-4 border-blue-500 opacity-70 rounded-full w-[10%] h-[10%] left-2/4 top-2/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {:else}
    <div class="absolute border border-blue-500 opacity-70 rounded-full w-[10%] h-[10%] left-2/4 top-2/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}
    
    <img id="micD" alt="microphone D" src={microphone} class="absolute w-[10%] h-[10%] z-0 left-1/4 top-3/4 -translate-y-2/4 -translate-x-2/4"/>
    <div class="absolute z-0 left-1/4 top-[65%] -translate-y-2/4 -translate-x-2/4 bg-white">{timeD}</div>
    {#if litD}
    <div class="absolute border-4 border-purple-500 opacity-70 rounded-full w-[10%] h-[10%] left-1/4 top-3/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {:else}
    <div class="absolute border border-purple-500 opacity-70 rounded-full w-[10%] h-[10%] left-1/4 top-3/4 -translate-y-2/4 -translate-x-2/4"> </div>
    {/if}

    {#if instruct}
    <div class="absolute text-center w-[40%] h-[5%] top-[15%] left-[25%] bg-white -translate-y-2/4 -translate-x-2/4 z-20 cursor-pointer pointer-events-none -rotate-12 text-blue-900 text-lg">Drag bird to move!</div>
    {/if}
    <div class="absolute bottom-0 w-24 left-2/4 -translate-x-2/4 px-2 py-1 bg-white text-xl z-40 border-t border-l border-r border-black">
        <div>{currentTimestamp}</div>
    </div>
</div>

<!-- timeline with coloured dots -->
<div class="relative grid grid-rows-[50%_50%] grid-cols-1 left-2/4 -translate-x-2/4 w-[30rem] h-12 mb-4">
    <div class="relative">
        <div class="absolute left-0 top-2/4 -translate-y-2/4">|</div>
        <div class="absolute left-1/4 top-2/4 -translate-y-2/4 -translate-x-2/4">|</div>
        <div class="absolute left-2/4 top-2/4 -translate-y-2/4 -translate-x-2/4">|</div>
        <div class="absolute left-3/4 top-2/4 -translate-y-2/4 -translate-x-2/4">|</div>
        <div class="absolute right-0 top-2/4 -translate-y-2/4">|</div>
        <div id="redbox" class="bg-orange-500 absolute left-0 top-2/4 -translate-y-2/4 -translate-x-2/4 2 h-4 w-4 rounded-full opacity-0"></div>
        <div id="greenbox" class="bg-green-500 absolute left-0 top-2/4 -translate-y-2/4 -translate-x-2/4 2 h-4 w-4 rounded-full opacity-0"></div>
        <div id="bluebox" class="bg-blue-500 absolute left-0 top-2/4 -translate-y-2/4 -translate-x-2/4 2 h-4 w-4 rounded-full opacity-0"></div>
        <div id="purplebox" class="bg-purple-500 absolute left-0 top-2/4 -translate-y-2/4 -translate-x-2/4 2 h-4 w-4 rounded-full opacity-0"></div>
    </div>
    <div class="relative">
        <div class="absolute left-0 top-2/4 -translate-y-2/4 -translate-x-2/4">0s</div>
        <div class="absolute left-1/4 top-2/4 -translate-y-2/4 -translate-x-2/4">1s</div>
        <div class="absolute left-2/4 top-2/4 -translate-y-2/4 -translate-x-2/4">2s</div>
        <div class="absolute left-3/4 top-2/4 -translate-y-2/4 -translate-x-2/4">3s</div>
        <div class="absolute right-0 top-2/4 -translate-y-2/4 -translate-x-2/4">4s</div>
    </div>
</div>
