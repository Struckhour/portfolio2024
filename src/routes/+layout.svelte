<script>
    import "../app.css";
    import { page } from "$app/stores";
    $: path = $page.url.pathname;
</script>
<!-- whole page -->
<div class="w-full min-h-lvh h-full bg-slate-100">
    <!-- nav bar -->
     <div class="fixed items-center w-full pr-20 z-50 h-20 opacity-90 bg-gradient-to-b from-white from-80% to-transparent">
        <div class="float-left flex items-center h-full">
            <div class="pl-20 grid grid-rows-2 grid-cols-1 gap-2">
                <div class="text-2xl text-center">
                    Luke McLean
                </div>
                <div>
                    Problem Solver, Researcher, Software Developer, Educator
                </div>
                
            </div>
        </div>
        <div class="float-right flex items-center h-full">
            <div class="grid grid-rows-1 grid-cols-3 gap-12 text-lg max-w-2xl">
                <a href="/" class={`mx-auto hover:underline active:text-slate-500 ${path === '/' ? "underline font-medium text-green-950": ""} `}>
                    Projects
                </a>
                <a href="/timeline" class={`mx-auto hover:underline active:text-slate-500 ${path === '/timeline' ? "underline font-medium text-green-950": ""} `}>
                    CV
                </a>
                <a href="/links" class={`mx-auto hover:underline active:text-slate-500 ${path === '/links' ? "underline font-medium text-green-950": ""} `}>
                    Links
                </a>
            </div>
        </div>

    </div>
    

    <slot />
</div>
