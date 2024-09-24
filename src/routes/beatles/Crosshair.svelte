<script>
    export let xAccessorScaled;
    export let yAccessorScaled;
    export let xLabel;
    export let yLabel;
    export let innerHeight;
  
      import * as d3 from "d3";
    const formatXLabel = d3.format('.0f');
      const formatYLabel = d3.format(',.1f');


      const albums = {
        1963.2: "Please Please Me",
        1963.9: "With The Beatles",
        1964.6: "A Hard Days Night",
        1964.95: "Beatles For Sale",
        1965.6: "Help!",
        1965.93: "Rubber Soul",
        1966.6: "Revolver",
        1967.2: "Sgt Peppers Lonely Hearts Club Band",
        1967.9: "Magical Mystery Tour",
        1968.5: "The Beatles",
        1969: "Let It Be",
        1969.6: "Abbey Road",
      }
  </script>
  
  <g transform={`translate(${xAccessorScaled} 0)`}>
    <text
      class="text-outline"
      y={innerHeight + 10}
      dy="0.8em"
      text-anchor={xLabel == 1969.6 ? "end" : "middle"}
    >
      {formatXLabel(xLabel)}
    </text>
    <text
      class="text"
      y={innerHeight + 10}
      dy="0.8em"
      text-anchor={xLabel == 1969.6 ? "end" : "middle"}
    >
      {Math.floor(xLabel)}-{albums[xLabel]}
    </text>
    <line
      class="line-outline"
      x1={0}
      x2={0}
      y1={yAccessorScaled}
      y2={innerHeight}
    />
    <line
      class="line"
      x1={0}
      x2={0}
      y1={yAccessorScaled}
      y2={innerHeight}
    />
  </g>
  
  <g transform={`translate(0 ${yAccessorScaled})`}>
    <text 
          class="text-outline" 
          dx={-10} 
          dy="0.34em" 
          text-anchor="end"
      >
      {formatYLabel(yLabel)}
    </text>
    <text 
          class="text" 
          dx={-10} 
          dy="0.34em" 
          text-anchor="end"
      >
      {formatYLabel(yLabel)}
    </text>
    <line
      class="line-outline"
      x1={xAccessorScaled}
      x2={0}
      y1={0}
      y2={0}
    />
    <line 
          class="line" 
          x1={xAccessorScaled} 
          x2={0} 
          y1={0} 
          y2={0} 
      />
  </g>
  
  <style>
    .text-outline {
      stroke: #ffffff;
      stroke-width: 8;
    }
  
    .text {
      fill: #a01357;
    }
  
    .line-outline {
      stroke: #ffffff;
      stroke-width: 3;
    }
  
    .line {
      stroke: #7c2650;
      stroke-width: 1;
    }
  </style>
  