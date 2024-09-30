<!-- App.svelte -->
<script lang="ts">
    import Ribbon from './ribbon.svelte';
    import Linepoints from './linepoints.svelte';
    const timeHeights = 
        [`top-[19%]`, `top-[39%]`, `top-[56%]`, `top-[75%]`,
        `top-[15%]`, `top-[27%]`, `top-[38%]`, `top-[55%]`, `top-[73%]`, `top-[90%]`];
    const dotSides = [`-translate-x-[100%]`, `-translate-x-[100%]`, `-translate-x-[100%]`, `-translate-x-[100%]`, 
        ``, ``, ``, ``, ``, 
    ]
    
    // const dates = [2024, 2023, 2022, 2021, 2020, 2019, 2012]
    // const dateHeights = [`top-[11%]`, `top-[25%]`, `top-[35%]`, `top-[45%]`,
    //     `top-[55%]`, `top-[65%]`, `top-[85%]`]

</script>



<div class="h-20 w-full"></div>
<div class="absolute w-full h-[1000px] max-w-4xl left-2/4 -translate-x-2/4 bg-slate-100">
    
    <div class="absolute left-2/4 -translate-x-2/4 w-[120px] sm:w-[200px] h-full">
        <Linepoints />
    </div>
    
    <!-- Education time points -->
    <div class="absolute w-2/4 right-2/4 h-full tracking-tight">
        <div class="absolute top-[2%] left-2/4 -translate-x-2/4 text-lg lg:text-2xl font-bold">Education</div>
        <div class="absolute text-center w-full px-8 xl:px-8 left-2/4 -translate-x-2/4 -translate-y-2/4 {timeHeights[0]} text-sm lg:text-lg tracking-tighter md:tracking-normal">
            <p class="font-bold text-green-900 font-serif tracking-widest">2022-2024</p>
            <p class="underline">Master's in Experimental Psychology</p>
            <p class="text-xs lg:text-base">major focus on coding complex data analysis and machine learning</p>
            <p class="text-xs lg:text-base">-University of New Brunswick-</p>
        </div>
        <div class="absolute text-center w-full px-8 xl:px-8 left-2/4 -translate-x-2/4 -translate-y-2/4 {timeHeights[1]} text-sm lg:text-lg tracking-tighter md:tracking-normal">
            <p class="font-bold text-green-900 font-serif tracking-widest">2022</p>
            <p class="underline">Coding Courses</p>
            <p class="text-xs lg:text-base">Python, Machine Learning, HTML/CSS, SQL, TypeScript, Vue, C#</p>
            <p class="text-xs lg:text-base">-Codecademy-</p>
        </div>
        <div class="absolute text-center w-full px-8 xl:px-8 left-2/4 -translate-x-2/4 -translate-y-2/4 {timeHeights[2]} text-sm lg:text-lg tracking-tighter md:tracking-normal">
            <p class="font-bold text-green-900 font-serif tracking-widest">2020-2021</p>
            <p class="underline">Bachelor of Education</p>
            <p class="text-xs lg:text-base">Math and Science</p>
            <p class="text-xs lg:text-base">-University of New Brunswick-</p>
        </div>
    
        <div class="absolute text-center w-full px-8 xl:px-8 left-2/4 -translate-x-2/4 -translate-y-2/4 {timeHeights[3]} text-sm lg:text-lg tracking-tighter md:tracking-normal">
            <p class="font-bold text-green-900 font-serif tracking-widest">2017-2020</p>
            <p class="underline">Bachelor of Science in Biopsychology (Hons)</p>
            <p class="text-xs lg:text-base">-University of New Brunswick-</p>
        </div>
    </div>
    
    <!-- work timepoints -->
    <div class="absolute w-2/4 left-2/4 h-full">
        <div class="absolute top-[2%] left-2/4 -translate-x-2/4 text-lg lg:text-2xl tracking-tight w-full text-center font-bold">Work Experience</div>
        <div class="absolute text-center w-full px-8 xl:px-8 left-2/4 -translate-x-2/4 -translate-y-2/4 {timeHeights[4]} text-sm lg:text-lg tracking-tighter md:tracking-normal">
            <p class="font-bold text-green-900 font-serif tracking-widest">2023-2024</p>
            <p class="underline">Research Assistant</p>
            <p class="text-xs lg:text-base">Psychology Research and Data Analysis</p>
            <p class="text-xs lg:text-base">-University of New Brunswick-</p>
        </div>
        <div class="absolute text-center w-full px-8 xl:px-8 left-2/4 -translate-x-2/4 -translate-y-2/4 {timeHeights[5]} text-sm lg:text-lg tracking-tighter md:tracking-normal">
            <p class="font-bold text-green-900 font-serif tracking-widest">2021-2024</p>
            <p class="underline">Freelance Web Developer</p>
            <p class="text-xs lg:text-base"></p>
            <p class="text-xs lg:text-base"></p>
        </div>
        <div class="absolute text-center w-full px-8 xl:px-8 left-2/4 -translate-x-2/4 -translate-y-2/4 {timeHeights[6]} text-sm lg:text-lg tracking-tighter md:tracking-normal">
            <p class="font-bold text-green-900 font-serif tracking-widest">2022-2023</p>
            <p class="underline">University Teaching Assistant</p>
            <p class="text-xs lg:text-base">Statistics and Psychology</p>
            <p class="text-xs lg:text-base">-University of New Brunswick-</p>
        </div>
        <div class="absolute text-center w-full px-8 xl:px-8 left-2/4 -translate-x-2/4 -translate-y-2/4 {timeHeights[7]} text-sm lg:text-lg tracking-tighter md:tracking-normal">
            <p class="font-bold text-green-900 font-serif tracking-widest">2021-2022</p>
            <p class="underline">High School Teacher</p>
            <p class="text-xs lg:text-base">Physics, Chemistry, and Music</p>
            <p class="text-xs lg:text-base">-St. Stephen High School-</p>
        </div>
        <div class="absolute text-center w-full px-8 xl:px-8 left-2/4 -translate-x-2/4 -translate-y-2/4 {timeHeights[8]} text-sm lg:text-lg tracking-tighter md:tracking-normal">
            <p class="font-bold text-green-900 font-serif tracking-widest">2019</p>
            <p class="underline">Research Assistant</p>
            <p class="text-xs lg:text-base">Data Collection and Analysis</p>
            <p class="text-xs lg:text-base">-University of New Brunswick-</p>
        </div>
        <div class="absolute text-center w-full px-8 xl:px-8 left-2/4 -translate-x-2/4 -translate-y-2/4 {timeHeights[9]} text-sm lg:text-lg tracking-tighter md:tracking-normal">
            <p class="font-bold text-green-900 font-serif tracking-widest">2012-2020</p>
            <p class="underline">Piano Teacher</p>
            <p class="text-xs lg:text-base">all ages, styles, and skill levels</p>
            <p class="text-xs lg:text-base">-St. Andrews, NB-</p>
        </div>
    </div>
    {#each timeHeights as height, index }
        <hr class="w-8 border-t-2 border-green-950 absolute left-2/4 {height} {dotSides[index]}">
    {/each}
    <!-- {#each dateHeights as height, index }
    <div class="bg-gray-100 border border-black bg-opacity-90 absolute left-2/4 {height} -translate-x-2/4 -translate-y-2/4 p-1">
        {dates[index]}
    </div>
    {/each} -->

</div>