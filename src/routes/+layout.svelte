<script>
    import "../app.css";
    import { page } from "$app/stores";

    $: path = $page.url.pathname;
    console.log(path);
</script>
<!-- whole page -->
<div class="w-full h-lvh">
    <!-- nav bar -->
     <div class="fixed w-full bg-white border-b border-green-900 z-50 h-10">
         <div class="flex text-lg justify-evenly my-2 mx-auto w-full max-w-2xl">
             <a href="/" class={`hover:underline active:text-slate-500 ${path === '/' ? "underline font-medium text-green-950": ""} `}>
                Home
            </a>

            <a href="/about" class={`hover:underline active:text-slate-500 ${path === '/about' ? "underline font-medium text-green-950": ""} `}>
                About
            </a>

            <a href='/projects' class={`hover:underline active:text-slate-500 ${path.includes('/projects') ? "underline font-medium text-green-950": ""} `}>
                Projects
            </a>
            
            <a href="/timeline" class={`hover:underline active:text-slate-500 ${path === '/timeline' ? "underline font-medium text-green-950": ""} `}>
                Timeline
            </a>
            
            <a href="/links" class={`hover:underline active:text-slate-500 ${path === '/links' ? "underline font-medium text-green-950": ""} `}>
                Links
            </a>
        </div>
    </div>
    <div class="h-10">
    </div>
    <slot />
</div>
