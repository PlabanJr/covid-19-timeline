<script>
  export let setCurrentCountry;

  let searchQuery = "";

  const changeCurrentCountry = () => {
    if (searchQuery.trim() === "") return;

    setCurrentCountry(searchQuery);
  };
</script>

<style>
  .search-bar-wrapper {
    width: 100%;
    display: flex;
    justify-content: space-between;
    box-sizing: border-box;
  }

  input {
    width: 100%;
  }

  button,
  input {
    padding: 10px 20px;
    font-size: 15px;
    border-radius: 5px;
    border: 1px solid #00756a;
    text-transform: uppercase;
    outline: none;
  }

  button {
    background: #00756a;
    color: #fff;
    margin-left: 10px;
    cursor: pointer;
  }
</style>

<div class="search-bar-wrapper">
  <input
    placeholder="Country name"
    bind:value={searchQuery}
    type="search"
    autocomplete="country-name" />
  <button on:click={changeCurrentCountry}>Search</button>
</div>
