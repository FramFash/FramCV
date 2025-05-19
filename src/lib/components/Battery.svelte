<!-- src/lib/BatteryDegradationChart.svelte -->
<script>
  import { onMount } from 'svelte';
  import * as d3 from 'd3';

  export let batteryData = [
    { 
      name: "Boosted Stealth", 
      data: [
        { month: 0, capacity: 100 },
        { month: 6, capacity: 95 },
        { month: 12, capacity: 88 },
        { month: 18, capacity: 82 },
        { month: 24, capacity: 75 }
      ]
    },
    { 
      name: "Evolve GTR", 
      data: [
        { month: 0, capacity: 100 },
        { month: 6, capacity: 97 },
        { month: 12, capacity: 93 },
        { month: 18, capacity: 89 },
        { month: 24, capacity: 85 }
      ]
    },
    { 
      name: "Meepo V4", 
      data: [
        { month: 0, capacity: 100 },
        { month: 6, capacity: 90 },
        { month: 12, capacity: 80 },
        { month: 18, capacity: 70 },
        { month: 24, capacity: 60 }
      ]
    }
  ];

  let tooltip = { show: false, content: "", x: 0, y: 0 };

  onMount(() => {
    const margin = { top: 40, right: 130, bottom: 60, left: 60 };
    const width = 800 - margin.left - margin.right;
    const height = 500 - margin.top - margin.bottom;

    const svg = d3.select("#linechart")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
      .append("g")
      .attr("transform", `translate(${margin.left},${margin.top})`);

    // Scales
    const x = d3.scaleLinear()
      .domain([0, d3.max(batteryData, d => d3.max(d.data, dd => dd.month))])
      .range([0, width]);

    const y = d3.scaleLinear()
      .domain([0, 100])
      .range([height, 0]);

    // Color scale
    const color = d3.scaleOrdinal(d3.schemeCategory10);

    // Axes
    svg.append("g")
      .attr("transform", `translate(0,${height})`)
      .call(d3.axisBottom(x).tickFormat(d => `${d} months`));

    svg.append("g")
      .call(d3.axisLeft(y).tickFormat(d => `${d}%`));

    // Axis labels
    svg.append("text")
      .attr("class", "axis-label")
      .attr("x", width / 2)
      .attr("y", height + margin.bottom - 10)
      .style("text-anchor", "middle")
      .style("fill", "white")
      .text("Time (months)");

    svg.append("text")
      .attr("class", "axis-label")
      .attr("transform", "rotate(-90)")
      .attr("x", -height / 2)
      .attr("y", -margin.left + 15)
      .style("text-anchor", "middle")
      .style("fill", "white")
      .text("Battery Capacity (%)");

    // Line generator
    const line = d3.line()
      .x(d => x(d.month))
      .y(d => y(d.capacity));

    // Add lines
    svg.selectAll(".line")
      .data(batteryData)
      .enter()
      .append("path")
      .attr("class", "line")
      .attr("d", d => line(d.data))
      .attr("stroke", d => color(d.name))
      .attr("stroke-width", 2)
      .attr("fill", "none");

    // Add dots
    svg.selectAll(".dot-group")
      .data(batteryData)
      .enter()
      .append("g")
      .attr("class", "dot-group")
      .selectAll(".dot")
      .data(d => d.data)
      .enter()
      .append("circle")
      .attr("class", "dot")
      .attr("cx", d => x(d.month))
      .attr("cy", d => y(d.capacity))
      .attr("r", 4)
      .attr("fill", (d, i, nodes) => color(nodes[i].parentNode.__data__.name))
      .on("mouseover", function(event, d) {
        const modelName = this.parentNode.__data__.name;
        tooltip = {
          show: true,
          content: `
            <strong>${modelName}</strong><br>
            Month: ${d.month}<br>
            Capacity: ${d.capacity}%
          `,
          x: event.pageX,
          y: event.pageY
        };
      })
      .on("mouseout", () => {
        tooltip.show = false;
      });

    // Legend
    const legend = svg.append("g")
      .attr("class", "legend")
      .attr("transform", `translate(${width + 20}, 20)`);

    batteryData.forEach((d, i) => {
      const legendItem = legend.append("g")
        .attr("transform", `translate(0, ${i * 20})`);

      legendItem.append("rect")
        .attr("width", 15)
        .attr("height", 15)
        .attr("fill", color(d.name));

      legendItem.append("text")
        .attr("x", 20)
        .attr("y", 12)
        .style("fill", "white")
        .text(d.name);
    });
  });
</script>

<style>
  .linechart-container {
    position: relative;
    width: 100%;
    margin: 2rem auto;
    overflow-x: scroll;
    display: flex;
    justify-content: center;
  }
  
  .line {
    fill: none;
    stroke-width: 2px;
  }
  
  .dot {
    stroke: white;
    stroke-width: 1px;
  }
  
  .axis-label {
    font-size: 14px;
    font-weight: bold;
  }
  
  .legend text {
    font-size: 12px;
  }
  
  .tooltip {
    position: absolute;
    padding: 8px;
    background: rgba(0, 0, 0, 0.8);
    color: white;
    border-radius: 4px;
    pointer-events: none;
    font-size: 12px;
    z-index: 10;
  }
  @media (max-width: 500px) {
    .linechart-container {
      display: block;
    }
  }
</style>

<div class="linechart-container">
  <svg id="linechart"></svg>
  {#if tooltip.show}
    <div class="tooltip" 
         style="left: {tooltip.x + 10}px; top: {tooltip.y - 28}px"
         innerHtml={tooltip.content}></div>
  {/if}
</div>
