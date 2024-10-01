<script>
    import "../app.css";
    import { page } from "$app/stores";
	import { goto } from "$app/navigation";
    $: path = $page.url.pathname;
</script>
<!-- whole page -->
<div class="w-full min-h-lvh h-full bg-slate-100">
    <!-- nav bar -->
     <div class="fixed items-center w-full pr-20 z-50 h-20 opacity-80 bg-gradient-to-b text-white from-black from-80% to-transparent">
        <div class="float-left hidden lg:flex items-center h-full">
            <button on:click={()=>goto('/')} class="pl-20 grid grid-rows-2 grid-cols-1 hover:cursor-pointer">
                <div class="text-2xl text-center flex items-end justify-center">
                    Luke McLean
                </div>
                <div class="sm:flex hidden text-lg items-start justify-center">
                    Problem Solver, Researcher, Software Developer, Educator
                </div>
                
            </button>
        </div>
        <div class="float-right flex items-center h-full">
            <div class="grid grid-rows-1 grid-cols-3 gap-12 text-xl max-w-2xl">
                <a href="/" class={`mx-auto hover:underline active:text-slate-500 ${path === '/' ? "underline font-medium text-green-200": ""} `}>
                    Projects
                </a>
                <a href="/timeline" class={`mx-auto hover:underline active:text-slate-500 ${path === '/timeline' ? "underline font-medium text-green-200": ""} `}>
                    CV
                </a>
                <a href="/links" class={`mx-auto hover:underline active:text-slate-500 ${path === '/links' ? "underline font-medium text-green-200": ""} `}>
                    Links
                </a>
            </div>
        </div>

    </div>
    

    <slot />
</div>
