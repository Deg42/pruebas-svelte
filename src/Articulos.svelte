<script>
    import { getContext, onMount } from "svelte";
    import { jsonData } from "./store";
    import Articulo from "./Articulo.svelte";
    import Buscar from "./Buscar.svelte";

    const URL = getContext("URL");
    let busqueda = "";
    
    onMount(() => {
        fetch(URL.articulos)
            .then((response) => response.json())
            .then((data) => ($jsonData = data));
    });

$: regexp = new RegExp (busqueda, "i");
$: datos = busqueda 
    ? $jsonData.filter((i) => regexp.test(i.nombre)) 
    : $jsonData
</script>

<h1>ARTICULOS</h1>

<Buscar bind:busqueda />

{#each datos as articulo}
    <Articulo {articulo} />
{/each}
