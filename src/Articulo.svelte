<script>
    export let articulo = {};
</script>

<div>
    <input type="text" bind:value={articulo.nombre} />
    <input type="text" bind:value={articulo.precio} />
    <slot/>
</div>