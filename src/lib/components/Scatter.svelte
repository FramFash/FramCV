<!-- src/lib/PricePerformanceScatter.svelte -->
<script>
  import { onMount, afterUpdate } from 'svelte';
  import * as d3 from 'd3';

  export let skateboards = [
    {
      name: "Wowgo 3E",
      img: "https://wowgoboard.com/cdn/shop/products/wowgo-3e-electric-skateboard-longboard-668434.jpg?v=1743667627",
      price: 439,
      battery: "12S2P 216Wh 43.2V 5.0Ah",
      top_speed: 45,
      range: 21,
      weight: 7.5,
      max_load: 150,
    },
    {
      name: "Wowgo 2S Max",
      img: "https://wowgoboard.com/cdn/shop/products/wowgo-2s-max-electric-skateboard-longboard-194722.jpg?v=1743667572",
      price: 399,
      battery: "12S2P 216Wh",
      top_speed: 45,
      range: 23,
      weight: 8.2,
      max_load: 150,
    },
    {
      name: "Maxfind Max 5s",
      img: "https://www.maxfind.com/cdn/shop/files/MAXFIND-MAX5-_NEW_-Maxfind-9692.jpg?v=1705550233&width=1000",
      price: 439,
      battery: "Samsung 18650 10S2P, 4.4Ah, 158.4Wh, 36V",
      top_speed: 40,
      range: 25,
      weight: 9.3,
      max_load: 150,
    },
    {
      name: "Meepo Edge",
      img: "https://www.meepoboard.com/cdn/shop/files/meepoedge6.jpg?v=1742806232&width=1080",
      price: 519,
      battery: "345.6Wh 8Ah",
      top_speed: 42,
      range: 32,
      weight: 9.0,
      max_load: 150,
    },
    {
      name: "Tynee Mini 3 SL",
      img: "https://tyneeboard.com/cdn/shop/files/Tynee-Mini-3-SL-Electric-Skateboard-With-105mm-Wheels-2_1600x.jpg?v=1744362407",
      price: 399,
      battery: "6Ah 216WH / 8Ah 288WH",
      top_speed: 45,
      range: 32,
      weight: 8.4,
      max_load: 150,
    },
    {
      name: "Backfire Nalu",
      img: "https://www.backfireboards.com/cdn/shop/files/Cube-S1_1024x1024.jpg?v=1728398122",
      price: 599,
      battery: "136.8Wh 30.4V 4.5Ah",
      top_speed: 25,
      range: 20,
      weight: 5.8,
      max_load: 110,
    },
    {
      name: "Exway Wave Riot",
      img: "https://tremor.fun/cdn/shop/files/ExwayWaveRiotTopandBottom_1080x_a06e35dd-8b5a-4a33-b6af-d1268f00e499.jpg?v=1694130189",
      price: 739,
      battery: "144Wh, 10S2p 42V 24A Smart BMW",
      top_speed: 38,
      range: 20,
      weight: 6.9,
      max_load: 200,
    },
    {
      name: "Meepo Go",
      img: "https://www.meepoboard.com/cdn/shop/files/MEEPOGO6.jpg?v=1739775641&width=1080",
      price: 529,
      battery: "50.4V -12S2P /345Wh/8Ah",
      top_speed: 45,
      range: 32,
      weight: 9.0,
      max_load: 150,
    },
    {
      name: "Exway Flex 2024 SE",
      img: "data:image/jpeg;base64,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",
      price: 649,
      battery: "216Wh 12S2P 51V 40Ah Smart BMS",
      top_speed: 45,
      range: 28,
      weight: 7.9,
      max_load: 150,
    },
    {
      name: "Meepo FLow",
      img: "https://www.meepoboard.com/cdn/shop/files/Flow_8ce9e5db-31c9-4c8c-82cd-60d198b18955.jpg?v=1739511723&width=1080",
      price: 699,
      battery: "50.4V - 12S2P molicel P42A 362Wh / 8.4Ah",
      top_speed: 52,
      range: 38,
      weight: 9.7,
      max_load: 150,
    },
    {
      name: "Propel Pivot GT",
      img: "https://www.ridepropel.com/wp-content/uploads/2023/06/pivot-S-2.png",
      price: 999,
      battery: "864Wh Samsung Cells 12S4P 50S",
      top_speed: 60,
      range: 87,
      weight: 14.5,
      max_load: 150,
    },
    {
      name: "Wowgo AT 2 Plus",
      img: "https://wowgoboard.com/cdn/shop/products/wowgo-at2-plus-electric-skateboard-longboard-443859.jpg?v=1743667876",
      price: 899,
      battery: "604Wh 14Ah 12S4P configuration",
      top_speed: 50,
      range: 45,
      weight: 13.6,
      max_load: 150,
    },
    {
      name: "Propel Endeavor 3S",
      img: "https://www.ridepropel.com/wp-content/uploads/2024/04/END-3S-1.png",
      price: 999,
      battery: "12S4P Lishen LR2170LA 48 cells",
      top_speed: 55,
      range: 38,
      weight: 20,
      max_load: 150,
    },
    {
      name: "Meepo Voyager X Limited",
      img: "https://www.meepoboard.com/cdn/shop/files/voyager_xl_4bb4bfab-7f21-4e4a-bc20-ee41e3698ad1.jpg?v=1739511903&width=2048",
      price: 1099,
      battery: "12S4P Lishen LR2170LA 48 cells",
      top_speed: 60,
      range: 49,
      weight: 11,
      max_load: 150,
    },
    {
      name: "Meepo Vader",
      img: "https://www.meepoboard.com/cdn/shop/files/Vader-Hurricane_Carbon.jpg?v=1739511611&width=1080",
      price: 1599,
      battery: "12S4P Samsung 50S (864Wh / 20Ah)",
      top_speed: 52,
      range: 50,
      weight: 17.6,
      max_load: 250,
    },
    {
      name: "Acedeck Nomad N3",
      img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQCmKNyaTK7gfZmQ7wZXx2YsY3JfG1pUqLr-g&s",
      price: 1424,
      battery: "14S6P Samsung 50E",
      top_speed: 60,
      range: 90,
      weight: 20.1,
      max_load: 150,
    },
    {
      name: "Acedeck Nyx Z3",
      img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQhCSjE5J6dKH4zsztafJbHNz0XzHvLzzYA5zBhHvCk9sPT6A4nRPPOCpMumPN1s1mgxcY&usqp=CAU",
      price: 1599,
      battery: "14S6P Samsung 50E",
      top_speed: 60,
      range: 95,
      weight: 22.1,
      max_load: 150,
    },
    {
      name: "Propel X4R",
      img: "https://www.ridepropel.com/wp-content/uploads/2024/05/X4R-%E6%B8%B2%E6%9F%931.png",
      price: 2799,
      battery: "Samsung 50S 12S7P 1512Wh 5000Mah",
      top_speed: 60,
      range: 68,
      weight: 45.0,
      max_load: 150,
    },
    {
      name: "Ownboard Carbon Zeus Pro",
      img: "https://www.ownboard.net/cdn/shop/files/Capture00122-2_1024x1024.jpg?v=1708313499",
      price: 1399,
      battery: "Samsung 50S 21700 13S4P 20Ah 936Wh",
      top_speed: 60,
      range: 80,
      weight: 13.0,
      max_load: 150,
    },
    {
      name: "Ownboard W2 PRO",
      img: "https://www.ownboard.net/cdn/shop/products/OwnboardElectricSkateboardW2PROWITH90PUwheels-_4_1200x1200.jpg?v=1702553754",
      price: 579,
      battery: "21700 sP12S 8.0Ah 345.6Wh",
      top_speed: 45,
      range: 30,
      weight: 8.8,
      max_load: 120,
    },
    {
      name: "Ownboard Prometheus Electric",
      img: "https://www.ownboard.net/cdn/shop/files/8C3A4448_1200x1200.jpg?v=1727663452",
      price: 1749,
      battery: "Samsung 50S 12S5P 25Ah 1170Wh",
      top_speed: 60,
      range: 80,
      weight: 20.5,
      max_load: 120,
    },
    {
      name: "Ownboard Mini KT",
      img: "https://www.ownboard.net/cdn/shop/products/8_176367fd-ea6d-46eb-81a8-a533b5035569_800x.jpg?v=1702553690",
      price: 369,
      battery: "18650 & 21700, 2P10S",
      top_speed: 40,
      range: 30.5,
      weight: 7.6,
      max_load: 120,
    },
    {
      name: "Evolve Renegade Diablo",
      img: "https://www.rideevolve.com/cdn/shop/files/Main_White_3.jpg?v=1719381890",
      price: 2299,
      battery: "43.2v - 864Wh - 20Ah - Samsung 50S",
      top_speed: 50,
      range: 50,
      weight: 16.4,
      max_load: 120,
    },
    {
      name: "Evolve Diablo Bamboo Street",
      img: "https://cdn.accentuate.io/8214050406536/1719137335284/Diablo_Bamboo_2in1_Collection.jpg?v=1719137335284",
      price: 1999,
      battery: "Samsung 50S",
      top_speed: 50,
      range: 50,
      weight: 15.3,
      max_load: 120,
    },
    {
      name: "Evolve Stoke X",
      img: "https://www.rideevolve.com/cdn/shop/files/STOKEX-08790-Edit_1024x1024.webp",
      price: 1399,
      battery: "12S2P - 43.2v - 432Wh - 10Ah - Samsung 50S",
      top_speed: 42,
      range: 45,
      weight: 10.5,
      max_load: 100,
    },
    {
      name: "Evolve GTR Bamboo",
      img: "https://www.rideevolve.com/cdn/shop/files/GTR-BAMBOO-CLEAR-82-Edit.jpg?v=1740544513",
      price: 1399,
      battery: "14Ah - 504Wh - 10S4P - 18650 Cells",
      top_speed: 38,
      range: 30,
      weight: 12.1,
      max_load: 100,
    },
  ];

  let tooltip = { show: false, content: "", x: 0, y: 0 };
  let svgInitialized = false;

  function renderChart() {
    // Skip if no data
    if (!skateboards || skateboards.length === 0) return;

    const margin = { top: 40, right: 130, bottom: 60, left: 60 };
    const width = 800 - margin.left - margin.right;
    const height = 500 - margin.top - margin.bottom;

    // Clear previous SVG if it exists
    const container = d3.select("#scatterplot-container");
    container.select("svg").remove();

    const svg = container
      .append("svg")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
      .append("g")
      .attr("transform", `translate(${margin.left},${margin.top})`);

    // Safely calculate domains
    const priceValues = skateboards.map(d => d.price).filter(Boolean);
    const rangeValues = skateboards.map(d => d.range).filter(Boolean);
    const speedValues = skateboards.map(d => d.top_speed).filter(Boolean);
    const weightValues = skateboards.map(d => d.weight).filter(Boolean);

    if (priceValues.length === 0 || rangeValues.length === 0) return;

    // Scales with fallbacks
    const x = d3.scaleLinear()
      .domain([0, d3.max(priceValues) * 1.1 || 1000])
      .range([0, width]);

    const y = d3.scaleLinear()
      .domain([0, d3.max(rangeValues) * 1.1 || 100])
      .range([height, 0]);

    // Color and size scales with fallbacks
    const color = d3.scaleSequential(d3.interpolateViridis)
      .domain([d3.min(speedValues) || 0, d3.max(speedValues) || 30]);

    const size = d3.scaleLinear()
      .domain([d3.min(weightValues) || 10, d3.max(weightValues) || 30])
      .range([5, 15]);

    // Axes
    svg.append("g")
      .attr("transform", `translate(0,${height})`)
      .call(d3.axisBottom(x).tickFormat(d => `$${d}`));

    svg.append("g")
      .call(d3.axisLeft(y));

    // Axis labels
    svg.append("text")
      .attr("class", "axis-label")
      .attr("x", width / 2)
      .attr("y", height + margin.bottom - 10)
      .style("text-anchor", "middle")
      .style("fill", "white")
      .text("Price (USD)");

    svg.append("text")
      .attr("class", "axis-label")
      .attr("transform", "rotate(-90)")
      .attr("x", -height / 2)
      .attr("y", -margin.left + 15)
      .style("text-anchor", "middle")
      .style("fill", "white")
      .text("Range (miles)");

    // Dots
    svg.selectAll(".dot")
      .data(skateboards)
      .enter()
      .append("circle")
      .attr("class", "dot")
      .attr("cx", d => x(d.price || 0))
      .attr("cy", d => y(d.range || 0))
      .attr("r", d => size(d.weight || 15))
      .style("fill", d => color(d.top_speed || 15))
      .on("mouseover", function(event, d) {
        tooltip = {
          show: true,
          content: `
            <strong>${d.name || 'Unknown'}</strong><br>
            Price: $${d.price || 'N/A'}<br>
            Range: ${d.range || 'N/A'} miles<br>
            Top Speed: ${d.top_speed || 'N/A'} mph<br>
            Weight: ${d.weight || 'N/A'} lbs
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
      .attr("transform", `translate(${width + 20}, 20)`);

    const legendScale = d3.scaleLinear()
      .domain([d3.min(speedValues) || 0, d3.max(speedValues) || 30])
      .range([0, 100]);

    legend.append("g")
      .call(d3.axisRight(legendScale).tickFormat(d => `${d} mph`))
      .select(".domain")
      .remove();

    legend.selectAll(".legend-color")
      .data(d3.range(30))
      .enter()
      .append("rect")
      .attr("x", -20)
      .attr("y", d => 100 - d * 3.33)
      .attr("width", 15)
      .attr("height", 3.33)
      .attr("fill", d => color(legendScale.invert(d * 3.33)));

    svgInitialized = true;
  }

  onMount(renderChart);
  afterUpdate(renderChart);
</script>

<style>
  .scatterplot-container {
    position: relative;
    width: 100%;
    margin: 2rem auto;
    overflow-x: scroll;
    display: flex;
    justify-content: center;
  }
  
  .dot {
    opacity: 0.8;
    stroke: #fff;
    transition: opacity 0.2s;
  }
  
  .dot:hover {
    opacity: 1;
    stroke: #000;
  }
  
  .axis-label {
    font-size: 14px;
    font-weight: bold;
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
  
  .no-data {
    text-align: center;
    padding: 2rem;
    color: #666;
  }

  @media (max-width: 500px) {
    .scatterplot-container {
      display: block;
    }
  }
</style>

<div id="scatterplot-container" class="scatterplot-container">
  {#if skateboards.length === 0}
    <div class="no-data">No skateboard data available</div>
  {/if}
  
  {#if tooltip.show}
    <div class="tooltip" 
         style="left: {tooltip.x + 10}px; top: {tooltip.y - 28}px"
         bind:this={tooltipElement}></div>
  {/if}
</div>

<script context="module">
  export function load({ data }) {
    return {
      props: {
        skateboards: data.skateboards || []
      }
    };
  }
</script>
