<script>
  import axios from "axios";
  import { onMount } from "svelte";

  import AllInformation from "../components/information.svelte";
  import AllInformationChart from "../components/information-chart.svelte";
  import Loading from "../components/loading.svelte";
  import PolarChart from "../components/polarChart.svelte";
  import DetailInfo from "../components/detailInfo.svelte";

  let data = {},
    responseData = {},
    loadingAll = true,
    loadingAllHistorical = true;

  onMount(() => {
    axios
      .get("https://corona.lmao.ninja/v2/all")
      .then(res => {
        data = res.data;
        loadingAll = false;
      })
      .catch(error => console.error(error));

    axios
      .get("https://corona.lmao.ninja/v2/historical/all")
      .then(res => {
        loadingAllHistorical = false;
        responseData = res.data;
      })
      .catch(error => console.error(error));
  });
</script>

<style>
  .body-wrapper {
    display: flex;
    flex-direction: column;
    padding: 50px;
  }

  .charts {
    display: flex;
    justify-content: space-around;
    flex-direction: column;
    padding-top: 30px;
  }

  @media (min-width: 720px) {
    .body-wrapper {
      padding: 50px 110px;
    }
  }

  @media (min-width: 1028px) {
    .charts {
      flex-direction: row;
    }
  }
</style>

<div class="body-wrapper">
  <AllInformation
    {data}
    loading={loadingAll}
    header="GLOBAL"
    hideClass={false} />

  <div class="charts">
    {#if loadingAll}
      <Loading />
    {:else}
      <PolarChart {data} />
      <DetailInfo {data} />
    {/if}
  </div>

  {#if loadingAllHistorical}
    <Loading />
  {:else}
    <AllInformationChart {responseData} />
  {/if}
</div>
