<script>
  import { onMount } from "svelte";
  import { fade } from "svelte/transition";
  import axios from "axios";
  import Chart from "chart.js";

  export let responseData = {};
  export let loading;

  let cases, trendChart;

  const renderCharts = () => {
    cases.height = 450;
    trendChart = new Chart(cases, {
      type: "line",
      data: {
        labels: Object.keys(responseData.cases),
        datasets: [
          {
            data: Object.values(responseData.cases),
            label: "Total Cases",
            borderColor: "red",
            fill: false
          },
          {
            data: Object.values(responseData.deaths),
            label: "Deaths",
            borderColor: "blue",
            fill: false
          },
          {
            data: Object.values(responseData.recovered),
            label: "Recovered",
            borderColor: "green",
            fill: false
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

  $: if (loading === false) renderCharts();
</script>

<style>
  .chart-wrapper {
    padding: 0px 110px 50px;
    height: 450px;
    display: flex;
    flex-direction: column;
  }

  .placeholder {
    height: 450px;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-size: 30px;
    padding-top: 100px;
  }

  .placeholder img {
    height: 120px;
  }
</style>

<div class="chart-wrapper">
  {#if loading}
    <div class="placeholder">
      <img src="Corona.svg" alt="logo" />
      LOADING...
    </div>
  {/if}
  <canvas id="cases" bind:this={cases} in:fade={{ duration: 800 }} />
</div>
