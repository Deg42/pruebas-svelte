<script>
    import { onMount, getContext } from "svelte";

    export let tipo = "insertar";
    export let coleccion = "articulos";

    let URL = getContext("URL");

    let clases = "insertar";
    let handler = () => {};
    let url = "";

    function insertar() {}
    function modificar() {}
    function eliminar() {}

    onMount(() => {
        switch (tipo) {
            case "insertar":
                clases = "insertar";
                handler = insertar;
                break;
            case "modificar":
                clases = "modificar";
                handler = modificar;
                break;
            case "eliminar":
                clases = "eliminar";
                handler = eliminar;
                break;
            default:
                clases = "insertar";
                break;
        }

        switch (coleccion) {
            case "articulos":
                url = URL.articulos;
                break;
            case "clientes":
                url = URL.clientes;
                break;
            default:
                break;
        }
    });
</script>

<button class={clases} on:click={handler} />

<style>
    .insertar {
        background-color: lightgreen;
    }
    .insertar::after {
        content: "Insertar";
    }

    .modificar {
        background-color: lightskyblue;
    }
    .modificar::after {
        content: "Modificar";
    }

    .eliminar {
        background-color: lightcoral;
    }
    .eliminar::after {
        content: "Borrar";
    }
</style>
