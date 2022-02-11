<script>
    import { getContext, onMount } from "svelte";
    import { jsonData } from "./store";
    import Articulo from "./Articulo.svelte";

    const URL = getContext("URL");

    onMount(() => {
        fetch(URL.articulos)
            .then((response) => response.json())
            .then((data) => ($jsonData = data));
    });
</script>

<h1>ARTICULOS</h1>

{#each $jsonData as articulo}
    <Articulo articulo = {articulo}/>
{/each}
