<script>
    import { getContext, onMount } from "svelte";
    import { jsonData } from "./store";
    import Articulo from "./Articulo.svelte";
    import Buscar from "./Buscar.svelte";
    import Boton from "./Boton.svelte";

    const URL = getContext("URL");
    let busqueda = "";
    let articulo = {};

    onMount(() => {
        fetch(URL.articulos)
            .then((response) => response.json())
            .then((data) => ($jsonData = data));
    });

    $: regexp = new RegExp(busqueda, "i");
    $: datos = busqueda
        ? $jsonData.filter((item) => regexp.test(item.nombre))
        : $jsonData;
</script>

<h1>ARTICULOS</h1>

<Buscar bind:busqueda={busqueda}/>
<Articulo bind:articulo={articulo}>
    <Boton tipo="insertar" coleccion="articulos" documento={articulo}/>
</Articulo>

{#each datos as articulo}
    <Articulo {articulo}>
        <Boton tipo="modificar" coleccion="articulos" documento={articulo} />
        <Boton tipo="eliminar" coleccion="articulos" documento={articulo} />
    </Articulo>
{/each}
