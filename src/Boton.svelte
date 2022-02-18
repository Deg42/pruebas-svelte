<script>
    import { onMount, getContext } from "svelte";
    import { jsonData } from "./store";

    export let tipo = "";
    export let coleccion = "articulos";
    export let documento = {};

    let URL = getContext("URL");

    let clases = "insertar";
    let handler = () => {};
    let url = "";

    function insertar () {  
    fetch(URL.articulos, 
    {
        method : "POST",
        headers: { "Content-type": "application/json" },
        body: JSON.stringify(documento)
    })
    .then( res => res.json() )
    .then( data =>  $jsonData = [ ...$jsonData, data ] );
 }

    function modificar() {}
    
    function eliminar() {
        fetch(url + documento._id, { method: "DELETE" })
            .then((response) => response.json())
            .then(
                (data) =>
                    ($jsonData = $jsonData.filter(
                        (x) => x._id !== documento._id
                    ))
            );
    }

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
