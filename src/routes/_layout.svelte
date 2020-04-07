<script>
  import NavBar from "../components/navigationBar.svelte";
  import FooterView from "../components/footer.svelte";

  export let segment;
</script>

<style>
  main {
    position: relative;
    background-color: white;
    margin: 0 auto;
    box-sizing: border-box;
    width: 100%;
  }
</style>

<NavBar {segment} />

<main>
  <slot />
</main>

<FooterView />
