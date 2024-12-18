<script>
    import * as d3 from "d3";
    import { interpolateString } from "d3-interpolate";
    import { draw, fade } from "svelte/transition";
    import { tweened } from 'svelte/motion'
    import Tooltip from "./Tooltip.svelte";
    
    // Receive plot and yaxis data as prop.
    export let data;
    export let y;
    export let colour;
  
    // The chart dimensions and margins as optional props.
    export let width = 1000;
    export let height = 350;
    export let marginTop = 20;
    export let marginRight = 30;
    export let marginBottom = 30;
    export let marginLeft = 50;

    let tooltipEvent;
  
    // Create the x (horizontal position) scale.
    let xScale = d3.scaleUtc(
      d3.extent(data, (d) => d.DATE),
      [marginLeft, width - marginRight]
    );
  
    // Create the y (vertical position) scale.
    $: yScale = d3.scaleLinear(
      [0, d3.max(data, (d) => +d[y])],
      [height - marginBottom, marginTop]
    );
  
    // Create the line generator.
    $: line = d3
      .line()
      .x((d) => xScale(d.DATE))
      .y((d) => yScale(+d[y]));
    
    $: path = line(data)

    function tickLabelFormatter(tick) {
      const number = Number(tick) / 1000000
      return number + 'M'
    }

    let animated_path = tweened(null, {
      interpolate: interpolateString,
      duration: 500,
    })

    $: animated_path.set(path)
    
  </script>
  
  <svg
    {width}
    {height}
    viewBox="0 0 {width} {height}"
    style:max-width="100%"
    style:height="auto"
    on:mousemove={(event) => tooltipEvent = event}
    on:mouseleave={() => tooltipEvent = null}
  >

  <g class=chart-container
  >
    <!-- X-Axis -->
    <g transform="translate(0,{height - marginBottom})">
      <line transition:fade={{delay:1000, duration:500}} stroke="black" x1={marginLeft - 6} x2={width} />
  
      {#each xScale.ticks() as tick}
        <!-- X-Axis Ticks -->
        <line
          transition:fade={{delay:1000, duration:500}}
          stroke="black"
          x1={xScale(tick)}
          x2={xScale(tick)}
          y1={0}
          y2={6}
        />
  
        <!-- X-Axis Tick Labels -->
        <text transition:fade={{delay:1000, duration:500}} fill="black" text-anchor="middle" x={xScale(tick)} y={22}>
          {tick.getFullYear()}
        </text>
      {/each}
    </g>
  
    <!-- Y-Axis and Grid Lines -->
    <g transform="translate({marginLeft},0)">
      {#each yScale.ticks(4) as tick}
        {#if tick !== 0}
          <!-- 
            Grid Lines. 
            Note: First line is skipped since the x-axis is already present at 0. 
          -->
          <line

            stroke="black"
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
            stroke="black"
            stroke-opacity="0.1"
            x1={0}
            x2={-6}
            y1={yScale(tick)}
            y2={yScale(tick)}
          />
        {/if}
  
        <!-- Y-Axis Tick Labels -->
        <text
          fill="black"
          text-anchor="end"
          dominant-baseline="middle"
          x={-9}
          y={yScale(tick)}
        >
          {tickLabelFormatter(tick)}
        </text>
      {/each}
    </g>
  
    <path
      transition:draw={{duration: 1500}} fill="none" stroke={colour} stroke-width="3" d={$animated_path} />
    {#if tooltipEvent && tooltipEvent.offsetX >= xScale.range()[0] && tooltipEvent.offsetX <= xScale.range()[1]}
      <line x1={tooltipEvent.offsetX+3} x2={tooltipEvent.offsetX+3} y1={marginTop} y2={height-marginBottom} style="stroke:black;stroke-width:1"></line>
    {/if}
  </g>
  </svg>

  {#if tooltipEvent && tooltipEvent.offsetX >= xScale.range()[0] && tooltipEvent.offsetX <= xScale.range()[1]}
    <Tooltip x=1050 y=1000 {data} {xScale} keys={[y]} bind:tooltipEvent={tooltipEvent}/>
  {/if}