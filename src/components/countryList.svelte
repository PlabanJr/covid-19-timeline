<script>
  import Loading from "./loading.svelte";

  export let countries;
  export let setCurrentCountry;
  export let loading;

  const changeCurrentCountry = country => {
    setCurrentCountry(country);
  };
</script>

<style>
  ul {
    list-style-type: none;
    padding: 0;
    height: 520px;
    overflow: auto;
    display: flex;
    flex-direction: column;
  }

  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: 1px solid #ddd;
    padding: 10px 20px;
    margin: 3px 0;
    border-radius: 10px;
    cursor: pointer;
  }

  li:hover {
    background: #f7f7f7;
    color: #00756a;
  }

  h3,
  h4 {
    margin: 0;
  }

  .country-detail {
    display: flex;
  }

  img {
    height: 20px;
    width: 30px;
    margin-right: 15px;
  }

  .cases {
    color: red;
  }
</style>

<ul>
  {#if loading}
    <Loading />
  {:else}
    {#each countries as { country, countryInfo, cases } (country)}
      <li on:click={changeCurrentCountry(country)} id={country.toUpperCase()}>
        <div class="country-detail">
          <img src={countryInfo.flag} alt="er" />
          <h3>{country}</h3>
        </div>
        <h4 class="cases">{cases}</h4>
      </li>
    {/each}
  {/if}
</ul>
