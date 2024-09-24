<script lang='ts'>
	import * as d3 from "d3";
	
  export let yScale;
	export let innerWidth;
	export let hoveredPoint;
  export let label;
  export let perc;

  let formatTick = d3.format(".1%");
  $: {
    if (!perc) {
      formatTick = d3.format(",.2r");
    } else {
      formatTick = d3.format(".1%");
    }
  }


  const numberOfTicks = (pixelsAvailable: number, pixelsPerTick = 60) =>
    Math.floor(Math.abs(pixelsAvailable) / pixelsPerTick);
	
  $: [yMin, yMax] = yScale.range();

  $: ticks = yScale.ticks(numberOfTicks(yMax - yMin));
</script>

<g>
  {#each ticks as tick}
    <g transform={`translate(0 ${yScale(tick)})`}>
      <line 
				x1={0} 
				x2={innerWidth}
				stroke='#bdc3c7'
				stroke-opacity='0.5'
			/>
      <text
        dx={-10}
        dy="0.34em"
        text-anchor="end"
        fill={hoveredPoint ? '#bdc3c7' : '#282828'}
      >
        {perc ? formatTick(tick/100) : formatTick(tick)}
      </text>
    </g>
  {/each}
  <text
		dx={0}
		y={-35} 
		dy="0.8em"
		text-anchor="start"
		fill='#282828'
	> 
    {label}
  </text>
</g>
