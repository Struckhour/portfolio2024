<script lang='ts'>
	export let selectedTheme: string;
	import { themes } from '$lib/themes';

	let menuOpen = false;
	const menuItems = Object.keys(themes);	
</script>


<section class="dropdown">
  <button class="bg-orange-700 px-4 py-4 rounded-lg text-white" on:click={() => menuOpen = !menuOpen}>Themes</button>
	
  <div id="myDropdown" class:show={menuOpen} class="dropdown-content">		

	<div class="just-words">

		<!-- MENU -->
        {#each Object.keys(themes) as listTheme}
            <button class="w-full block hover:bg-orange-200" on:click={()=>{selectedTheme = listTheme;menuOpen = false}}>{listTheme}</button>
        {/each}
	</div>
  </div>	
</section>
	
	
<style>		
.dropdown {
  position: relative;
  display: inline-block;
}
	
.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f6f6f6;
  min-width: 230px;
  border: 1px solid #ddd;
  z-index: 1;
  
}

/* Show the dropdown menu */	
.show {display:block;}	
</style>