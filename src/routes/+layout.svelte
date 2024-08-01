<script>
    import "../app.css";
    import { page } from "$app/stores";

    $: path = $page.url.pathname;
    console.log(path);
</script>
<!-- whole page -->
<div class="w-full min-h-lvh h-full bg-slate-100">
    <!-- nav bar -->
     <div class="fixed w-full bg-white border-b border-green-900 z-50 h-10">
         <div class="flex text-lg justify-evenly my-2 mx-auto w-full max-w-2xl">
             <a href="/" class={`hover:underline active:text-slate-500 ${path === '/' ? "underline font-medium text-green-950": ""} `}>
                Projects
            </a>
            
            <a href="/timeline" class={`hover:underline active:text-slate-500 ${path === '/timeline' ? "underline font-medium text-green-950": ""} `}>
                Timeline/CV
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
