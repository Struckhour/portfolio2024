<script lang='ts'>
	import * as d3 from "d3";

	import Line from './Line.svelte';
	import XAxis from './XAxis.svelte';
	import GridLines from './GridLines.svelte';
	import Crosshair from './Crosshair.svelte';
	import Point from './Point.svelte';
	
  export let perc;
	export let stats;
  export let title;

	let hoveredPoint: number | null = null;

	const margin = {
    top: 50,
    right: 50,
    bottom: 50,
    left: 80,
  };

	let width = 100;
  $: height = 0.50 * width;

  $: innerWidth = width - margin.left - margin.right;
  $: innerHeight = height - margin.top - margin.bottom;

	const xAccessor = d => d.year;
  const yAccessor = d => d.statistic;

	const bisectX = d3.bisector(xAccessor).left;

	$: xScale = d3
    .scaleLinear()
    .domain(d3.extent(stats, xAccessor))
    .range([0, innerWidth]);

	$: yScale = d3
    .scaleLinear()
    .domain(d3.extent(stats, yAccessor))
    .range([innerHeight, 0])
    .nice();

	$: xAccessorScaled = d => xScale(xAccessor(d));
  const yAccessorScaled = d => yScale(yAccessor(d));

	const handleMouseMove = event => {
    const xCoordinate = xScale.invert(event.offsetX - margin.left);
    const index = bisectX(stats, xCoordinate);
    hoveredPoint = stats[index - 1];
  };

  const handleMouseLeave = () => {
    hoveredPoint = null;
  };
</script>

<div 
	class="wrapper" 
	bind:clientWidth={width}
>
  <svg 
		role="img"
    aria-label="line chart that shows how Beatles lyrics changed over time" 
		{width} 
		{height}
		on:mousemove={handleMouseMove}
    on:mouseleave={handleMouseLeave}
	>
    <g transform={`translate(${margin.left}, ${margin.top})`}>
		  <XAxis
        {xScale}
				{innerHeight}
				{hoveredPoint}
        label="Recording Date"
      />
			<GridLines
        {yScale}
				{innerWidth}
				{hoveredPoint}
        label={title}
        perc={perc}
      />
      <Line 
				{stats}
				{xAccessorScaled}
				{yAccessorScaled}
			/>
			{#if hoveredPoint}
				<Crosshair
          xAccessorScaled={xAccessorScaled(hoveredPoint)}
          yAccessorScaled={yAccessorScaled(hoveredPoint)}
          xLabel={xAccessor(hoveredPoint)}
          yLabel={yAccessor(hoveredPoint)}
					{innerHeight}
        />
        <Point
          x={xAccessorScaled(hoveredPoint)}
          y={yAccessorScaled(hoveredPoint)}
          color="#dc267f"
        />
      {/if}
    </g>
  </svg>
</div>

<style>
  .wrapper {
    position: relative;
    width: 100%;
    max-width: 900px;
  }
</style>
