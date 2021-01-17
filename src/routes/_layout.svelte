<script>
  import Nav from "../components/Nav.svelte";

  export let segment;
</script>

<style>
  main {
    width: 100vw;
    height: 100vh;
  }
</style>

<main>
  <slot />
</main>
