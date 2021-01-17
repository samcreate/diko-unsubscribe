<script>
  import Nav from "../components/Nav.svelte";

  export let segment;
</script>

<style>
  main {
    width: 100vw;
    height: 100vh;
  }
  @media only screen and (max-width: 39.1875rem) {
    main {
      width: 100%;
      height: 100%;
      min-height: -webkit-fill-available;
    }
  }
</style>

<main>
  <slot />
</main>
