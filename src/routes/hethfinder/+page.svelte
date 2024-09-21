<script lang="ts">
    import earlyheth from '$lib/earlyheth.png';
    import lateheth from '$lib/lateheth.png';
    import notheth from '$lib/notheth.png';
    import lowheth from '$lib/lowheth.png';
    import highheth from '$lib/highheth.png';
    import noisyheth from '$lib/noisyheth.png';
</script>

<div class="max-w-3xl mx-auto mt-6 p-2 text-lg">
    <h1 class="text-center text-2xl text-green-950 mb-4">Birdsong Detection and Classification</h1>
    <p class="py-2 indent-4">Birdsong research often involves boxing and selecting a lot of songs on a computer screen&#x2014;sometimes thousands. To aid with this process, I used Python (with tensorflow) to build an image classifier that detects and boxes hermit thrush songs. This involved scraping years of data from our lab, using that data to train a machine learning model, then writing post-processing software to increase the accuracy and convert the output into <a class="underline" target="_blank" href="https://www.birds.cornell.edu/ccb/raven-pro/">Raven</a>  selection tables.</p>
    <p class="indent-4">For a simplified look what the program distinguishes, consider the spectrogram images below, some of which are left-aligned hermit thrush song (hits) and some of which are other birdsong or misaligned hermit thrush song (misses). With a strong signal and little background noise, the program typically identifies the timing and pitch of about 90-100% of the hermit thrush songs on a recording.</p>
    <div class="grid grid-cols-2 grid-rows-[12px_fr_fr_fr] gap-2 mt-4">
        <h2 class="text-center underline">Hits</h2>
        <h2 class="text-center underline">Misses</h2>
        <div>
            <h2 class="text-center text-sm">Left-aligned low-pitched hermit thrush song</h2>
            <img class="border-4 border-blue-500 w-full h-[200px] object-fill" alt="aligned spectrogram of low-pitched hermit thrush song" src={lowheth} />
        </div>
        <div>
            <h2 class="text-center text-sm">Same song, too far to the right</h2>
            <img class="border-4 border-red-500 w-full h-[200px] object-fill" alt="hermit thrush song too far to the right." src={lateheth} />
        </div>
        <div>
            <h2 class="text-center text-sm">Left-aligned high-pitched hermit thrush song</h2>
            <img class="border-4 border-blue-500 w-full h-[200px] object-fill" alt="aligned spectrogram of high-pitched hermit thrush song" src={highheth} />
        </div>
        <div>
            <h2 class="text-center text-sm">Same song, too far to the left</h2>
            <img class="border-4 border-red-500 w-full h-[200px] object-fill" alt="misaligned hermit thrush song too far to the left." src={earlyheth} />
        </div>
        <div>
            <h2 class="text-center text-sm">Left-aligned hermit thrush song with interference</h2>
            <img class="border-4 border-blue-500 w-full h-[200px] object-fill" alt="aligned spectrogram of noisy hermit thrush song" src={noisyheth} />
        </div>
        <div>
            <h2 class="text-center text-sm">Other birdsong (not hermit thrush)</h2>
            <img class="border-4 border-red-500 w-full h-[200px] object-fill" alt="other birdsong" src={notheth} />
        </div>
    </div>
    <p class="mt-12">To learn more about this process and the software, check out the <a href="https://www.youtube.com/watch?v=hOoyaQzYnX0&list=PLIWFDVILUKED29staaSbOvyotepbeH3fp" target="_blank" class="underline">youtube tutorial series</a> or the <a href="https://github.com/Struckhour/hethfinder" target="_blank" class="underline">code on github.</a></p>
    <div class="h-96"></div>
</div>