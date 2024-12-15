<script>
    import * as d3 from "d3";
    import Tooltip from "./Tooltip.svelte";
  
    // Receive plot and yaxis data as prop.
    export let data;
    export let keys;
    export let colors;
    export let hoveredSource;
  
    // The chart dimensions and margins as optional props.
    export let width = 1200;
    export let height = 550;
    export let marginTop = 20;
    export let marginRight = 30;
    export let marginBottom = 30;
    export let marginLeft = 50;

    let tooltipEvent;

	let stackedData = d3.stack()
		.keys(keys)
		(data)
  
    // Create the x (horizontal position) scale.
    const xScale = d3.scaleUtc(
      d3.extent(data, (d) => d.DATE),
      [marginLeft, width - marginRight]
    );
  
    // Create the y (vertical position) scale.
    const yScale = d3.scaleLinear(
      [0, d3.max(data, (d) => d.GENERATION)],
      [height - marginBottom, marginTop]
    );

    // Create the area generator.
    const area = d3
      .area()
      .x((d) => xScale(d.data.DATE))
      .y0((d)=> yScale(d[0]))
      .y1((d) => yScale(d[1]));

    function tickLabelFormatter(tick) {
      const number = Number(tick) / 1000000
      return number + 'M'
    }

  </script>
  
  <svg
    {width}
    {height}
  >
    <!-- X-Axis -->
    <g transform="translate(0,{height - marginBottom})">
      <line stroke="currentColor" x1={marginLeft - 6} x2={width} />
  
      {#each xScale.ticks() as tick}
        <!-- X-Axis Ticks -->
        <line
          stroke="currentColor"
          x1={xScale(tick)}
          x2={xScale(tick)}
          y1={0}
          y2={6}
        />
  
        <!-- X-Axis Tick Labels -->
        <text fill="currentColor" text-anchor="middle" x={xScale(tick)} y={22}>
          {tick.getFullYear()}
        </text>
      {/each}
    </g>
  
    <!-- Y-Axis and Grid Lines -->
    <g transform="translate({marginLeft},0)">
      {#each yScale.ticks(5) as tick}
        {#if tick !== 0}
          <!-- 
            Grid Lines. 
            Note: First line is skipped since the x-axis is already present at 0. 
          -->
          <line
            stroke="currentColor"
            stroke-opacity="0.1"
            x1={0}
            x2={width - marginLeft}
            y1={yScale(tick)}
            y2={yScale(tick)}
          />
  
          <!-- 
            Y-Axis Ticks. 
            Note: First tick is skipped since the x-axis already acts as a tick. 
          -->
          <line
            stroke="currentColor"
            x1={0}
            x2={-6}
            y1={yScale(tick)}
            y2={yScale(tick)}
          />
        {/if}
  
        <!-- Y-Axis Tick Labels -->
        <text
          fill="currentColor"
          text-anchor="end"
          dominant-baseline="middle"
          x={-9}
          y={yScale(tick)}
        >
          {tickLabelFormatter(tick)}
        </text>
      {/each}
  
      <!-- Y-Axis Label -->
      <text fill="currentColor" text-anchor="start" x={-marginLeft} y={15}>
    
      </text>
    </g>

    <g
      on:mouseleave={() => tooltipEvent = null}>
      {#each stackedData as source, i}
    <path
        fill={colors[source.key]}
        fill-opacity={hoveredSource === source.key ? 1.0 : hoveredSource ? 0.3 : 1.0}
        stroke="none"
        d={area(source)}
        on:mousemove={(event) => tooltipEvent = event}
    />
    {/each}
    </g>

    {#if tooltipEvent}
      <line x1={tooltipEvent.offsetX+3} x2={tooltipEvent.offsetX+3} y1={marginTop} y2={height-marginBottom} style="stroke:black;stroke-width:1"></line>
    {/if}
  </svg>

{#if tooltipEvent}
  <Tooltip {data} {xScale} {keys} bind:tooltipEvent={tooltipEvent}/>
{/if}