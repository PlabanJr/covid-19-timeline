<script>
  export let segment;

  const corona = "Corona.svg";

  $: console.log(segment);
</script>

<style>
  .logo {
    height: 3rem;
    width: 3rem;
    margin-right: 15px;
  }

  .left-header {
    display: flex;
    align-items: center;
  }

  .nav-list {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
    display: flex;
    align-items: center;
  }

  li {
    float: left;
    padding: 10px;
    font-size: 16px;
    cursor: pointer;
  }

  a {
    text-decoration: none;
    display: block;
  }

  [aria-current] {
    position: relative;
    display: inline-block;
  }

  [aria-current]::after {
    position: absolute;
    content: "";
    width: 100%;
    height: 2px;
    background-color: #fff;
    display: block;
    bottom: -1px;
  }

  nav {
    background: #00756a;
    color: #f5f5f5;
    padding: 15px 50px;
    font-weight: bold;
    font-size: 2rem;
    display: flex;
    justify-content: space-between;
  }

  img {
    height: 24px;
  }
</style>

<nav>
  <a href="/">
    <div class="left-header">
      <img src={corona} alt="Corona" class="logo" />
      <span>COVID 19</span>
    </div>
  </a>

  <ul class="nav-list">
    <li>
      <a aria-current={segment === undefined ? 'page' : undefined} href=".">
        GLOBAL
      </a>
    </li>
    <li>
      <a
        aria-current={segment === 'countries' ? 'page' : undefined}
        href="countries">
        COUNTRIES
      </a>
    </li>
    <li>
      <a
        aria-current={segment === 'graphs-charts' ? 'page' : undefined}
        href="graphs-charts">
        GRAPHS & CHARTS
      </a>
    </li>
    <li>
      <a
        aria-current={segment === 'symptoms-precautions' ? 'page' : undefined}
        href="symptoms-precautions">
        SYMPTOMS & PREVENTIONS
      </a>
    </li>
    <li>
      <a href="https://github.com/PlabanJr" target="_blank">
        <img src="github-image.svg" alt="github" />
      </a>
    </li>
    <li>
      <a href="https://twitter.com/plaban_jr" target="_blank">
        <img src="twitter.svg" alt="twitter" />
      </a>
    </li>
  </ul>
</nav>
