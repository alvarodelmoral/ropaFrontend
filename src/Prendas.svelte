<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";

  import Buscar                  from "./Buscar.svelte";
  import Prenda                  from "./Prenda.svelte";
  import Boton                   from "./Boton.svelte";

  const URL = getContext("URL");

  let busqueda = "";
  let prenda = {};

  onMount(async () => {
    const response = await fetch(URL.prendas);
    const data = await response.json();
    $jsonData = data;
  });

  $: regex = new RegExp(busqueda, "i");
  $: datos = busqueda 
    ? $jsonData.filter(item => regex.test(item.nombre))
    : $jsonData;

</script>

<style>
  .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: left;
    flex-wrap: wrap;
  }
</style>

<h1>PRENDAS</h1>
<Buscar bind:busqueda />

<div class="container">
  <Prenda bind:prenda>
    <div style="text-align: right">
      <Boton documento={prenda} tipo="insertar" coleccion="prendas" />
    </div>
  </Prenda>
</div>

<div class="container">
  {#each datos as prenda}
    <Prenda {prenda}>
      <div style="text-align: right">
        <Boton documento={prenda} tipo="modificar" coleccion="prendas" />
        <Boton documento={prenda} tipo="eliminar"  coleccion="prendas" />
      </div>
    </Prenda>
  {/each}
</div>
