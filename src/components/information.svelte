<script>
  import { onMount } from "svelte";
  import moment from "moment";
  import { fade } from "svelte/transition";

  export let loading;
  export let data = {};
  export let header;
  export let hideCases;

  const fadeInDuration = 800;
  const placeholderText = "---";

  moment.updateLocale("en", {
    relativeTime: {
      future: "in %s",
      past: "%s ago",
      s: "0 minutes",
      ss: "%d seconds",
      m: "a minute",
      mm: "%d minutes",
      h: "an hour",
      hh: "%d hours",
      d: "a day",
      dd: "%d days",
      M: "a month",
      MM: "%d months",
      y: "a year",
      yy: "%d years"
    }
  });

  $: totalCases = data.cases;
  $: activeCases = data.active;
  $: recoveredCases = data.recovered;
  $: deathCases = data.deaths;
  $: updatedAt = moment(data.updated);
  $: formatedTimestamp = updatedAt.fromNow();
</script>

<style>
  header {
    font-size: 2rem;
    padding-left: 10px;
  }

  .global-head {
    border-bottom: 2px solid #ddd;
    display: flex;
    justify-content: space-between;
    align-items: center;
    text-transform: uppercase;
    flex-direction: column;
  }

  .updated-at {
    display: flex;
    font-size: 12px;
    text-transform: uppercase;
  }

  .updated-at time {
    color: #00756a;
  }

  .wrapper {
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
  }

  h2,
  h1 {
    text-align: center;
  }

  .cards {
    border: 2px solid #ddd;
    border-radius: 10px;
    box-shadow: #ddd 2px 3px;
    width: 90%;
    padding: 20px;
    margin: 10px;
  }

  .total-cases {
    color: red;
  }

  .active-cases {
    color: blue;
  }

  .recovered-cases {
    color: green;
  }

  .death-cases {
    color: gray;
  }

  .placeholder {
    color: #ddd;
  }

  @media (min-width: 1028px) {
    .wrapper {
      flex-direction: row;
    }

    .cards {
      width: 100%;
    }
  }
  @media (min-width: 420px) {
    .updated-at {
      font-size: 15px;
    }

    .global-head {
      flex-direction: row;
    }
  }
</style>

<header id="information-header">
  <div class="global-head">
    {header}
    <div class="updated-at">
      LAST UPDATED:
      <time>{formatedTimestamp}</time>
    </div>
  </div>
</header>

<section class="wrapper">
  {#if !hideCases}
    <div class="total-cases cards">
      <h2 class="title">TOTAL</h2>
      {#if loading}
        <h1 class="placeholder">{placeholderText}</h1>
      {:else}
        <h1 in:fade={{ duration: fadeInDuration }}>{totalCases}</h1>
      {/if}
    </div>
  {/if}

  <div class="active-cases cards">
    <h2 class="title">ACTIVE</h2>
    {#if loading}
      <h1 class="placeholder">{placeholderText}</h1>
    {:else}
      <h1 in:fade={{ duration: fadeInDuration }}>{activeCases}</h1>
    {/if}
  </div>

  <div class="recovered-cases cards">
    <h2 class="title">RECOVERED</h2>
    {#if loading}
      <h1 class="placeholder">{placeholderText}</h1>
    {:else}
      <h1 in:fade={{ duration: fadeInDuration }}>{recoveredCases}</h1>
    {/if}
  </div>

  <div class="death-cases cards">
    <h2 class="title">DECEASED</h2>
    {#if loading}
      <h1 class="placeholder">{placeholderText}</h1>
    {:else}
      <h1 in:fade={{ duration: fadeInDuration }}>{deathCases}</h1>
    {/if}
  </div>
</section>
