<script>
  import SearchBar from "../components/searchBar.svelte";
  import Information from "../components/information.svelte";
  import InformationChart from "../components/information-chart.svelte";
</script>

<style>
  .wrapper {
    display: flex;
    justify-content: space-between;
    padding-top: 20px;
  }

  .left-wrapper {
    display: flex;
    flex-direction: column;
    flex: 2;
  }

  .right-wrapper {
    flex: 3;
  }
</style>

<div class="wrapper">
  <section class="left-wrapper">
    <Information data={{}} loading={true} />
    <SearchBar />
  </section>

  <section class="right-wrapper">
    <InformationChart responseData={{}} loading={true} />
  </section>
</div>
