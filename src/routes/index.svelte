<script>
  import axios from "axios";
  import { onMount } from "svelte";

  import AllInformation from "../components/information.svelte";
  import AllInformationChart from "../components/information-chart.svelte";

  let data = {},
    responseData = {},
    loadingAll = true,
    loadingAllHistorical = true;

  onMount(() => {
    axios
      .get("https://corona.lmao.ninja/all")
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
  }
</style>

<div class="body-wrapper">
  <AllInformation {data} loading={loadingAll} header={true} />
  <AllInformationChart {responseData} loading={loadingAllHistorical} />
</div>
