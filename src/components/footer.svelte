<script>
  const importantLinks = [
    {
      label: "WHO Covid-19",
      link: "https://www.who.int/emergencies/diseases/novel-coronavirus-2019"
    },
    {
      label: "WHO Advice for Public",
      link:
        "https://www.who.int/emergencies/diseases/novel-coronavirus-2019/advice-for-public"
    },
    {
      label: "WHO Covid QA's",
      link: "https://www.who.int/news-room/q-a-detail/q-a-coronaviruses"
    },
    {
      label: "WHO Research on COVID-19",
      link:
        "https://www.who.int/emergencies/diseases/novel-coronavirus-2019/global-research-on-novel-coronavirus-2019-ncov"
    },
    {
      label: "WHO Mythbusters",
      link:
        "https://www.who.int/emergencies/diseases/novel-coronavirus-2019/advice-for-public/myth-busters"
    },
    {
      label: "Govt. of India, COVID-19",
      link: "https://www.mygov.in/covid-19/?cbps=1"
    }
  ];
</script>

<style>
  footer,
  .row {
    background: #fddd;
    padding: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding-bottom: 0;
  }

  h3 {
    margin: 0;
    border-bottom: 2px solid #000;
  }

  ul {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
  }

  li {
    display: flex;
    align-items: center;
    float: left;
    margin: 20px;
    color: #00756a;
  }

  li img {
    height: 40px;
    width: 40px;
    margin-right: 10px;
  }

  p {
    width: 100%;
    text-align: center;
    margin: 0;
  }

  .data-source {
    color: #00756a;
  }

  .create-by {
    padding: 10px 0;
    background: #00756a;
    color: #fff;
  }

  .create-by a {
    color: #caecff;
  }

  @media (min-width: 1024px) {
    ul {
      flex-direction: row;
    }

    footer {
      padding: 20px 50px;
    }
  }
</style>

<footer>
  <div class="row">
    <h3>DO THE FIVE TO STAY SAFE</h3>
    <ul class="do-five-gif">
      <li>
        <img src="hand-wash.svg" alt="hand-wash" />
        Wash your HANDS often
      </li>
      <li>
        <img src="cough.svg" alt="cough" />
        Cough into ELBOW
      </li>
      <li>
        <img src="dont-touch.svg" alt="" />
        Don't touch FACE
      </li>
      <li>
        <img src="keep-distance.svg" alt="" />
        Keep safe distance
      </li>
      <li>
        <img src="family.svg" alt="" />
        Stay HOME
      </li>
    </ul>
  </div>

  <div class="row">
    <h3>IMPORTANT LINKS</h3>
    <ul class="do-five-gif">
      {#each importantLinks as { label, link }, i (i)}
        <li>
          <a href={link} target="_blank">{label}</a>
        </li>
      {/each}

    </ul>
  </div>

  <p class="data-source">
    <i>
      <a href="https://github.com/NovelCOVID/API" target="_blank">
        Data Source
      </a>
    </i>
  </p>
</footer>

<p class="create-by">
  Created by
  <i>
    <a href="https://github.com/PlabanJr" target="_blank">PlabanJr</a>
  </i>
</p>
