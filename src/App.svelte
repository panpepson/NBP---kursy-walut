<script>
  import NBP from "./Nbp.svelte";
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
  .pep {
    text-align: right;
    padding-top: 3rem;
  }
  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <NBP />
  <br />
  <div class="pep">
    Średni kurs walut nbp.pl
    <br />
    <a href="https://trochymiak.net">^p^</a>
  </div>
  power by
  <a href="https://svelte.dev" target="_blank">Svelte</a>
</main>
