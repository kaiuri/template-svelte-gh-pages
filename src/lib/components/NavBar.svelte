<!-- Automatically generates a NavBar using svelte/kit routes  -->
<script lang="ts">
  import { pipe } from "fp-ts/function";

  export let url: URL;
  const RouteRegex = new RegExp(/\/src\/routes(.*)\/\+page.svelte/);
  const routes = pipe(
    import.meta.glob("/src/routes/**/*.svelte"),
    (components) => Object.keys(components),
    (files) =>
      files.flatMap((route: string) => route.match(RouteRegex)?.[1] ?? ""),
    (routes) => Array.from(new Set(routes)),
    (routes) =>
      routes.flatMap((route) => ({
        name: route === "" ? "/HOME" : route.toUpperCase(),
        href: route === "" ? "/" : route,
      }))
  );
</script>

<header class="block">
  <nav class="block">
    <ul class="inline-block">
      {#each routes as p}
        <li class="inline-block text-2xl p-2">
          <a
            class={"hover:text-red-300 " +
              (url.pathname === p.href ? "font-bold" : "")}
            href={p.href}>{p.name}</a
          >
        </li>
      {/each}
    </ul>
  </nav>
</header>
