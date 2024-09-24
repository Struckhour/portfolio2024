<script>
	export let xScale;
	export let innerHeight;
	export let hoveredPoint;
	export let label;

	const numberOfTicks = (pixelsAvailable, pixelsPerTick = 70) =>
    Math.min(Math.floor(Math.abs(pixelsAvailable) / pixelsPerTick), 6);

  $: [xMin, xMax] = xScale.range();

  $: ticks = xScale.ticks(numberOfTicks(xMax - xMin));
</script>

<g transform={`translate(0 ${innerHeight})`}>
  <line 
		x1={xMin} 
		x2={xMax} 
		y1={0} 
		y2={0} 
		stroke='#bdc3c7'
	/>
  {#each ticks as tick}
    <g transform={`translate(${xScale(tick)} 0)`}>
      <line 
				y1={0} 
				y2={6} 
				stroke='#bdc3c7'
			/>
      <text
        y={10}
        dy="0.8em"
        text-anchor="middle"
        fill={hoveredPoint ? '#bdc3c7' : '#282828'}
      >
        {tick}
      </text>
    </g>
  {/each}
  <text
    x={xScale.range()[1] / 2}
    text-anchor="middle"
    y={45}
		fill='#282828'
  >
    {label}
  </text>
</g>
