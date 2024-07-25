<script lang="ts">
    import birdlocs from '$lib/jun22-2023.png';
    import consistency from '$lib/consistency.png';
	import { fade } from 'svelte/transition';


</script>

<div class="max-w-3xl mx-auto mt-6 p-2 text-lg">
    <h1 class="text-center text-2xl text-green-950 mb-4">Birdsong Detection and Classification</h1>
    <p class="py-2 indent-4">Birdsong research often involves boxing and selecting a lot of songs on a computer screen&#x2014;sometimes thousands. To aid with this process, I used Python (with tensorflow) to build an image classifier that detects and boxes hermit thrush songs. This involved scraping years of data from our lab, using that data to train a machine learning model, then writing post-processing software to increase the accuracy and convert the output into <a class="underline" href="https://www.birds.cornell.edu/ccb/raven-pro/">Raven</a>  selection tables.</p>
    <p class="indent-4">To understand what the model does, consider the spectrogram images below, some of which are left-aligned hermit thrush song (hits) and some of which are other birdsong or misaligned hermit thrush song (misses)</p>
    <div class="grid grid-cols-2 grid-rows-[12px_fr_fr_fr] gap-2 mt-4">
        <h2 class="text-center underline">Hits</h2>
        <h2 class="text-center underline">Misses</h2>
        <div>
            <h2 class="text-center text-sm">Aligned low-pitched hermit thrush song</h2>
            <img class="border border-green-500" alt="aligned spectrogram of low-pitched hermit thrush song" src={birdlocs} />
        </div>
        <div>
            <h2 class="text-center text-sm">Other birdsong (not hermit thrush)</h2>
            <img class="border border-red-500" alt="other birdsong" src={birdlocs} />
        </div>
        <div>
            <h2 class="text-center text-sm">Aligned high-pitched hermit thrush song</h2>
            <img class="border border-green-500" alt="aligned spectrogram of high-pitched hermit thrush song" src={birdlocs} />
        </div>
        <div>
            <h2 class="text-center text-sm">Too far to the left</h2>
            <img class="border border-red-500" alt="misaligned hermit thrush song too far to the left." src={birdlocs} />
        </div>
        <div>
            <h2 class="text-center text-sm">Aligned hermit thrush song with background noise</h2>
            <img class="border border-green-500" alt="aligned spectrogram of noisy hermit thrush song" src={birdlocs} />
        </div>
        <div>
            <h2 class="text-center text-sm">Too far to the right</h2>
            <img class="border border-red-500" alt="hermit thrush song too far to the right." src={birdlocs} />
        </div>
    </div>
    <p>To learn more about this process and the software, check out the youtube tutorial series or the code on github.</p>
    <div class="h-96"></div>
</div>