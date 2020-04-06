<script>
  import { onMount } from "svelte";
  import axios from "axios";
  import Chart from "chart.js";

  export let data = {};
  export let height = "450px";

  let deatilChart, trendChart;

  const renderCharts = () => {
    deatilChart.height = 450;
    trendChart = new Chart(deatilChart, {
      type: "pie",
      data: {
        labels: [
          "Cases today",
          "Deaths today",
          "Critical",
          "Cases per 1 million",
          "Deaths per 1 million",
          "Affected Countries"
        ],
        datasets: [
          {
            data: [
              data.todayCases,
              data.todayDeaths,
              data.critical,
              data.casesPerOneMillion,
              data.deathsPerOneMillion,
              data.affectedCountries
            ],
            backgroundColor: [
              "#3e95cd",
              "#ddd",
              "#8e5ea2",
              "#3cba9f",
              "#e8c3b9",
              "#c45850"
            ]
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
    padding: 10px 100px;
  }
</style>

<div class="chart-wrapper" style={`height: ${height}`}>
  <canvas bind:this={deatilChart} />
</div>
