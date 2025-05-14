<script>
  import * as d3 from 'd3';
  import { onMount, afterUpdate } from 'svelte';

  export let boards;
  export let selectedStat = 'range';
  
  let container;
  let svg;
  let width = 750;
  const height = 400;
  const margin = { top: 20, right: 20, bottom: 120, left: 60 };

  // Colors
  const colors = {
    axisLabels: 'white',
    bars: '#3b82f6',
    text: '#1f2937'
  };

  // Handle window resize
  const handleResize = () => {
    if (!container) return;
    
    // For mobile (under 600px), use fixed width to enable scrolling
    if (window.innerWidth < 600) {
      width = 750; // Minimum 350px or enough for all bars
    } 
    // For desktop, use container width
    else {
      width = container.clientWidth - margin.left - margin.right;
    }
    
    // Update SVG dimensions
    if (svg) {
      svg.setAttribute('width', width + margin.left + margin.right);
      svg.setAttribute('height', height + margin.top + margin.bottom);
    }
    
    drawChart();
  };

  onMount(() => {
    window.addEventListener('resize', handleResize);
    handleResize();
    return () => window.removeEventListener('resize', handleResize);
  });

  afterUpdate(() => {
    drawChart();
  });

  function drawChart() {
    if (!svg) return;

    d3.select(svg).selectAll("*").remove();

    const chart = d3.select(svg)
      .append("g")
      .attr("transform", `translate(${margin.left},${margin.top})`);

    // Create scales
    const x = d3.scaleBand()
      .domain(boards.map(d => d.name))
      .range([0, width])
      .padding(0.2);

    const maxValue = d3.max(boards, d => d[selectedStat]);
    const y = d3.scaleLinear()
      .domain([0, maxValue * 1.1])
      .nice()
      .range([height, 0]);

    // Add bars
    chart.selectAll(".bar")
      .data(boards)
      .enter()
      .append("rect")
      .attr("class", "bar")
      .attr("x", d => x(d.name))
      .attr("width", x.bandwidth())
      .attr("y", height)
      .attr("height", 0)
      .attr("fill", colors.bars)
      .style("cursor", "pointer")
      .style("transition", "fill 0.2s ease")
      .on("mouseover", function() {
        d3.select(this)
          .attr("fill", "#f74343");
      })
      .on("mouseout", function() {
        d3.select(this)
          .attr("fill", colors.bars);
      })
      .transition()
      .duration(500)
      .attr("y", d => y(d[selectedStat]))
      .attr("height", d => height - y(d[selectedStat]));

    // X-axis with rotated labels
    const xAxis = chart.append("g")
      .attr("transform", `translate(0,${height})`)
      .call(d3.axisBottom(x));

    xAxis.selectAll("text")
      .attr("transform", "rotate(-45)")
      .style("text-anchor", "end")
      .attr("dx", "-0.8em")
      .attr("dy", "0.15em")
      .style("fill", colors.axisLabels)
      .style("font-size", window.innerWidth < 600 ? "10px" : "12px");

    // Y-axis
    chart.append("g")
      .call(d3.axisLeft(y))
      .selectAll("text")
      .style("fill", colors.axisLabels);

    // Y-axis label
    chart.append("text")
      .attr("transform", "rotate(-90)")
      .attr("y", 0 - margin.left)
      .attr("x", 0 - (height / 2))
      .attr("dy", "1em")
      .style("text-anchor", "middle")
      .style("fill", colors.axisLabels)
      .text(getAxisLabel());
  }

  function getAxisLabel() {
    switch(selectedStat) {
      case 'price': return 'Precio (USD)';
      case 'range': return 'Rango (Km)';
      case 'top_speed': return 'Velocidad Máxima (km/h)';
      case 'weight': return 'Peso (kg)';
      default: return selectedStat;
    }
  }
</script>

<div class="stat-selector">
  <select bind:value={selectedStat}>
    <option value="range">Rango</option>
    <option value="top_speed">Velocidad Máxima</option>
    <option value="price">Precio</option>
    <option value="weight">Peso</option>
  </select>
</div>

<div class="chart-container" bind:this={container}>
  <div class="chart-wrapper">
    <svg bind:this={svg}></svg>
  </div>
</div>

<style>
  .chart-container {
    width: 100%;
    margin: 0 auto;
    font-family: sans-serif;
  }
  
  .chart-wrapper {
    width: 100%;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch; /* Smooth scrolling on iOS */
  }
  
  /* Desktop - fluid width */
  @media (min-width: 600px) {
    .chart-wrapper {
      overflow-x: visible;
    }
    svg {
      width: 100%;
    }
  }
  
  /* Mobile - fixed width with scrolling */
  @media (max-width: 600px) {
    svg {
      min-width: 100%;
      width: auto;
    }
  }
  
  .stat-selector {
    margin: 20px 0;
    text-align: center;
  }
  
  select {
    padding: 8px 12px;
    border-radius: 6px;
    border: 1px solid #d1d5db;
    background-color: black;
    color: white;
    font-size: 14px;
  }

  /* Mobile select */
  @media (max-width: 600px) {
    select {
      width: 100%;
      max-width: 300px;
      box-sizing: border-box;
    }
  }

  /* Chart styling */
  :global(.domain) {
    stroke: #d1d5db;
  }

  :global(.tick line) {
    stroke: #e5e7eb;
  }
</style>
