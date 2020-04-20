<script>
  import { onMount } from "svelte";
  import axios from "axios";

  import SearchBar from "../components/searchBar.svelte";
  import CountryList from "../components/countryList.svelte";
  import Information from "../components/information.svelte";
  import InformationChart from "../components/information-chart.svelte";
  import Loading from "../components/loading.svelte";

  const hideCases = true;
  let currentCountryData = {},
    countries = [],
    loading = true,
    chartLoading = true,
    responseData = {};

  onMount(() => {
    axios
      .get("https://corona.lmao.ninja/v2/countries")
      .then(response => {
        countries = response.data;
        currentCountryData = response.data[0];
        loading = false;
      })
      .then(() => getHistoricalData())
      .catch(e => console.error(e));
  });

  const getHistoricalData = (country = currentCountryData.country) => {
    chartLoading = true;

    axios
      .get("https://corona.lmao.ninja/v2/historical/" + country)
      .then(response => {
        responseData = response.data.timeline;
        chartLoading = false;
      })
      .catch(e => console.error(e));
  };

  const setCurrentCountry = currentCountry => {
    getHistoricalData(currentCountry);

    const infoHeader = document.getElementById("information-header");
    infoHeader.scrollIntoView({ behavior: "smooth", block: "start" });

    currentCountryData = countries.find(
      country => country.country.toLowerCase() === currentCountry.toLowerCase()
    );
  };
</script>

<style>
  .wrapper {
    display: flex;
    justify-content: space-between;
    padding-top: 50px;
    flex-direction: column;
  }

  .left-wrapper,
  .right-wrapper {
    display: flex;
    flex-direction: column;
    flex: 2;
    padding: 0px 25px;
  }

  .right-wrapper {
    padding: 0px 25px;
  }

  @media (min-width: 1028px) {
    .wrapper {
      flex-direction: row;
      padding: 50px 120px 0px 120px;
    }
  }
</style>

<div class="wrapper">
  <section class="left-wrapper">
    <SearchBar {setCurrentCountry} />
    <CountryList {countries} {setCurrentCountry} {loading} />
  </section>

  <section class="right-wrapper">
    <Information
      data={currentCountryData}
      {loading}
      header={currentCountryData.country || 'country'}
      hideCases={true} />

    {#if chartLoading}
      <Loading />
    {:else}
      <InformationChart
        title={'Historical Data of ' + currentCountryData.country}
        {responseData}
        height="350px" />
    {/if}
  </section>
</div>
