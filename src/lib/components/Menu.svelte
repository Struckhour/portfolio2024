<script lang='ts'>
	import Link from './Link.svelte';
	import Button from './Button.svelte';
	import Input from './Input.svelte';
	export let filterList: string[];
	import beatlesLyrics from '$lib/beatles_lyrics.json';

	let menuOpen = false;
	let inputValue = "";
	$:console.log(inputValue)
	$:test = 'test';

	const menuItems = beatlesLyrics['columns'].slice(5, -1);
	// const menuItems = ["About", "Base", "Blog", "Contact", "you", "Support", "Tools", "Boats", "Cars", "Bikes", "Sheds", "Billygoats", "Zebras", "Tennis Shoes", "New Zealand"];
	let filteredItems: string[] = [];
	
	const handleInput = () => {
		return filteredItems = menuItems.filter(item => item.toLowerCase().match(inputValue.toLowerCase()));	
	}
</script>


<section class="dropdown">
  <Button on:click={() => menuOpen = !menuOpen} {menuOpen} />
	
  <div id="myDropdown" class:show={menuOpen} class="dropdown-content">		
  <Input bind:inputValue on:input={handleInput} />
	<div class="just-words">

		<!-- MENU -->
		{#if filteredItems.length > 0}
			{#each filteredItems as item}
				{#if filterList.includes(item)}
					<button class="block bg-blue-500 border-b border-slate-100 w-full">{item}</button>
				{:else}
					<button class="block hover:bg-slate-200 border-b border-slate-100 w-full" on:click={() => filterList = [...filterList, item]}>{item}</button>
				{/if}
			{/each}
		{:else}
			{#each menuItems as item}
				{#if filterList.includes(item)}
					<button class="block bg-blue-500 border-b border-slate-100 w-full">{item}</button>
				{:else}
					<button class="block hover:bg-slate-200 border-b border-slate-100 w-full" on:click={() => filterList = [...filterList, item]}>{item}</button>
				{/if}
			{/each}
		{/if}		
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

.just-words {
	overflow-y: scroll;
	max-height: 300px;
}

/* Show the dropdown menu */	
.show {display:block;}	
</style>