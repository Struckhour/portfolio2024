<script lang='ts'>
	import Youtube from "svelte-youtube-embed";

  let overlayBGColor = "#e5a50a";
  let overlayTransitionDuration = 50;

  let titleColor = "#000000";
  let titleShadowColor = "#ffffff";
  let titleFontFamily = "'Segoe UI', Geneva, Verdana, sans-serif";

  let altThumb = false;
</script>

<div class="container">
  <Youtube id="o3RUdRO-_Yo" />

</div>

<style>
  .container {
    max-width: 800px;
    margin: 0 auto;
    padding-left: 1rem;
    padding-right: 1rem;
  }
  ul {
    display: flex;
    list-style: none;
    padding: 0;
  }
  li {
    margin-right: 1rem;
  }
  .controls {
    display: flex;
    align-items: center;
    margin: 1rem auto;
  }
  .controls label {
    font-weight: bold;
  }

	input[type="checkbox"] {
		display: inline-block;
		margin-left: 10px;
		margin-top: 10px;
	}
</style>
