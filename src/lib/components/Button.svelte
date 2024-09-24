<script>
	export let menuOpen;
</script>

<style>	
/* Dropdown Button */
.dropbtn {
  color: white;
  padding: 16px;
  font-size: 16px;
  border: none;
  cursor: pointer;
}
	


</style>

<button on:click class="dropbtn rounded-lg hover:bg-green-800 bg-cyan-700 focus:bg-green-800">{!menuOpen ? "Words" : "Close"}</button>
