<script>
  import { onMount } from "svelte";
  import axios from "axios";
  import Chart from "chart.js";

  export let data = {};
  export let height = "450px";

  let polarChart, trendChart;

  const renderCharts = () => {
    polarChart.height = 450;
    trendChart = new Chart(polarChart, {
      type: "polarArea",
      data: {
        labels: ["Total", "Active", "Recovered", "Deaths"],
        datasets: [
          {
            data: [data.cases, data.active, data.recovered, data.deaths],
            backgroundColor: ["blue", "red", "green", "#ddd"]
          }
        ]
      },
      options: {
        maintainAspectRatio: false
      }
    });

    trendChart.render({
      duration: 1000,
      lazy: true,
      easing: "linear"
    });
  };

  onMount(() => renderCharts());
</script>

<style>
  .chart-wrapper {
    border: 1px solid #ddd;
    border-radius: 10px;
    padding: 10px;
  }

  @media (min-width: 720px) {
    .chart-wrapper {
      padding: 10px 100px;
    }
  }
</style>

<div class="chart-wrapper" style={`height: ${height}`}>
  <canvas bind:this={polarChart} />
</div>
