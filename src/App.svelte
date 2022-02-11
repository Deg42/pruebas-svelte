<script>
	import Nav from "./Nav.svelte";
	import Contenido from "./Contenido.svelte";
	import { Router } from "svelte-routing";

	import { setContext } from "svelte";

	const URL = {
		articulos: "https://tiendabackend.herokuapp.com/api/articulos/",
		clientes: "https://tiendabackend.herokuapp.com/api/clientes/",
	};

	setContext("URL", URL);
</script>

<Router>
	<Nav />
	<Contenido />
</Router>
