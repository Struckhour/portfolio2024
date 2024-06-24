<script>
    import "../app.css";
</script>
<!-- whole page -->
<div class="w-full h-lvh">
    <!-- nav bar -->
    <div class="flex text-lg justify-evenly my-2 mx-auto w-full max-w-2xl">
        <a href="/" class="hover:underline active:text-slate-500">
            Home
        </a>

        <a href="/about" class="hover:underline active:text-slate-500">
            About
        </a>

        <a href='/projects' class="hover:underline active:text-slate-500">
            Projects
        </a>

        <a href="/timeline" class="hover:underline active:text-slate-500">
            Timeline
        </a>

        <a href="/links" class="hover:underline active:text-slate-500">
            Links
        </a>


    </div>
    <hr class="border-t border-slate-300 w-full max-w-2xl mx-auto">
    <slot />
</div>
