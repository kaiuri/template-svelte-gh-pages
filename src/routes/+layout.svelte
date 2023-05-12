<script lang="ts">
  import "../app.css";
  import NavBar from "$lib/components/NavBar.svelte";
  import { page } from "$app/stores";

  let width: number;
  let height: number;
</script>

<svelte:window bind:outerHeight={height} bind:outerWidth={width} />
<svelte:head>
  <title>{$page.url.pathname}</title>
</svelte:head>

<NavBar url={$page.url} />

<main class="block">
  <slot />
</main>

<style>
  :global(body) {
    background-color: theme("colors.cyan.800");
  }
  header {
    background-color: theme("colors.cyan.900");
  }
  main {
    padding: theme("spacing.4");
  }
  :global(nav) {
    padding: theme("spacing.4");
    background-color: theme("colors.cyan.900");
  }
  :global(p) {
    color: theme("colors.cyan.100");
  }
  :global(h1, h2, h3, h4, h5, h6) {
    color: theme("colors.cyan.100");
    font-weight: theme("fontWeight.bold");
  }
  :global(a) {
    color: theme("colors.cyan.400");
  }
</style>
