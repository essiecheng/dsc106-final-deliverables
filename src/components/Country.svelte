<script>
  import { onMount } from 'svelte';
  import * as d3 from 'd3';

  let points = [];
  const spacing = 12;
  let radius = 4;
  let pointsPerSideX;
  let totalGeneratedPoints;
  let data = [];
  let tooltipData = null;
  let hoveredPoint = null;

  async function fetchData() {
    const resForward = await fetch('olympic.csv');
    const csvForward = await resForward.text();
    data = d3.csvParse(csvForward, d3.autoType);
    generatePoints();
  }

  onMount(() => {
    fetchData();
  });

  function generatePoints() {
    points = [];

    const filteredData = data.filter(
      (d) =>
        d.Country_Code === 'USA' ||
        d.Country_Code === 'URS' ||
        d.Country_Code === 'AUS'
    );

    const medalCounts = {
      USA: 0,
      URS: 0,
      AUS: 0,
    };

    filteredData.forEach((d) => {
      if (d.Country_Code === 'USA') medalCounts.USA++;
      else if (d.Country_Code === 'URS') medalCounts.URS++;
      else if (d.Country_Code === 'AUS') medalCounts.AUS++;
    });

    totalGeneratedPoints = medalCounts.USA + medalCounts.URS + medalCounts.AUS;
    pointsPerSideX = Math.ceil(Math.sqrt(totalGeneratedPoints) * 1.5);

    let currentX = 0;
    let currentY = 0;

    // points
    generatePointsForCountry(medalCounts.USA, 'USA');
    generatePointsForCountry(medalCounts.URS, 'URS');
    generatePointsForCountry(medalCounts.AUS, 'AUS');

    function generatePointsForCountry(count, country) {
      const countryData = filteredData.filter(
        (d) => d.Country_Code === country
      );
      for (let i = 0; i < count; i++) {
        points.push({
          x: currentX * spacing + radius,
          y: currentY * spacing + radius,
          country,
          tooltip: countryData[i],
          index: points.length,
        });

        currentX++;
        if (currentX >= pointsPerSideX) {
          currentX = 0;
          currentY++;
        }
      }
    }
  }

  function showTooltip(data) {
    tooltipData = data.tooltip;
    hoveredPoint = data.index;
  }

  function hideTooltip() {
    tooltipData = null;
    hoveredPoint = null;
  }
</script>

<div class="container">
  <div class="text-container">
    <p>1. United States</p>
    <p>1992 medals</p>
    <br /><br /><br /><br /><br />
    <p>2. Soviet Union</p>
    <p>1021 medals</p>
    <br />
    <p>3. Australia</p>
    <p>798 medals</p>
  </div>

  <svg width="800" height="800">
    {#each points as point, i}
      <g on:mouseenter={() => showTooltip(point)} on:mouseleave={hideTooltip}>
        <circle
          cx={point.x}
          cy={point.y}
          r={point.index === hoveredPoint ? radius * 2.5 : radius}
          fill={point.country === 'USA'
            ? '#DEC70D'
            : point.country === 'URS'
              ? '#A5A1A1'
              : '#C67C03'}
        />
        {#if tooltipData === point.tooltip}
          <title>
            {`City: ${point.tooltip.City}, Year: ${point.tooltip.Year}, Sport: ${point.tooltip.Sport}, Event: ${point.tooltip.Event}, Athlete: ${point.tooltip.Athlete}, Gender: ${point.tooltip.Gender}, Medal: ${point.tooltip.Medal}`}
          </title>
        {/if}
      </g>
    {/each}
  </svg>
</div>

{#if tooltipData}
  <div class="tooltip">
    <p>Country: {tooltipData.Country}</p>
    <p>City: {tooltipData.City}</p>
    <p>Year: {tooltipData.Year}</p>
    <p>Sport: {tooltipData.Sport}</p>
    <p>Event: {tooltipData.Event}</p>
    <p>Athlete: {tooltipData.Athlete}</p>
    <p>Gender: {tooltipData.Gender}</p>
    <p>Medal: {tooltipData.Medal}</p>
  </div>
{/if}

<style>
  .tooltip {
    position: relative;
    background-color: white;
    border: 1px solid #aaa;
    padding: 10px;
    pointer-events: none;
    z-index: 999;
    font-size: 20px;
    right: -1020px;
    top: -800px;
    width: 300px;
  }

  .container {
    display: flex;
    justify-content: center;
    margin-right: 300px;
  }

  .text-container {
    margin-right: 20px;
    font-size: 20px;
    color: white;
  }
</style>
