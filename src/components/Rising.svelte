<script>
  import { onMount } from 'svelte';
  import { tweened } from 'svelte/motion';
  import { draw, fade } from 'svelte/transition';
  import { extent } from 'd3-array';
  import { scaleLinear } from 'd3-scale';
  import { line, curveBasis } from 'd3-shape';

  export let data;
  export let title;
  export let show;

  let xScale, yScale, pathLine;

  function createChart() {
    xScale = scaleLinear()
      .domain(extent(data.map((d) => d.year)))
      .range([5, 95]);

    yScale = scaleLinear()
      .domain(extent(data.map((d) => d.count)))
      .range([5, 75]);

    pathLine = line()
      .x((d) => xScale(d.year))
      .y((d) => yScale(d.count))
      .curve(curveBasis);
  }

  onMount(createChart);
  $: createChart();
</script>

<div class="plot-container">
  <h3>{title}</h3>
  <br />
  <br />
  <svg class="plot">
    {#if show}
      <path transition:draw={{ duration: 2000 }} d={pathLine(data)} />
    {/if}
  </svg>
</div>

<style>
  path {
    stroke: purple;
    stroke-width: 2;
    fill: none;
    stroke-linecap: round;
  }
  .plot-container {
    display: flex;
    justify-content: center;
    margin-left: -150px;
    margin-right: 0px;
  }
</style>
