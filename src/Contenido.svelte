<script>
  import { Route }  from "svelte-routing";
  import Inicio     from "./Inicio.svelte";
  import Prendas    from "./Prendas.svelte";
  import Clientes   from "./Clientes.svelte";
</script>

<style>
  main {
    padding: 20px;
    padding-top: 50px;
  }
</style>

<main id="contenido">
  <Route path="/" component={Inicio} />
  <Route path="/prendas" component={Prendas} />
  <Route path="/clientes" component={Clientes} />
</main>
