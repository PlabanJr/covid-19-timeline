<script>
  import { onMount } from "svelte";
  import axios from "axios";
  import Chart from "chart.js";

  export let responseData = {};
  export let height = "450px";
  export let title = "Global Historical Data";

  let cases, trendChart;

  const renderCharts = () => {
    cases.height = 450;
    trendChart = new Chart(cases, {
      type: "line",
      data: {
        labels: Object.keys(responseData.cases) || [0, 1, 2],
        datasets: [
          {
            data: Object.values(responseData.cases) || [0, 0, 0],
            label: "Total Cases",
            borderColor: "red",
            fill: false
          },
          {
            data: Object.values(responseData.deaths) || [0, 0, 0],
            label: "Deaths",
            borderColor: "blue",
            fill: false
          },
          {
            data: Object.values(responseData.recovered) || [0, 0, 0],
            label: "Recovered",
            borderColor: "green",
            fill: false
          }
        ]
      },
      options: {
        maintainAspectRatio: false,
        title: {
          display: true,
          text: title
        }
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
    height: 450px;
    display: flex;
    flex-direction: column;
    padding-top: 20px;
  }
</style>

<div class="chart-wrapper" style={`height: ${height}`}>
  <canvas id="cases" bind:this={cases} />
</div>
