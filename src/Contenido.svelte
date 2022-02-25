<script>
  import { Route }  from "svelte-routing";
  import Inicio     from "./Inicio.svelte";
  import Distribuidores  from "./Distribuidores.svelte";
  import Plantas   from "./Plantas.svelte";
</script>

<style>
  main {
    padding: 20px;
    padding-top: 50px;
  }
</style>

<main id="contenido">
  <Route path="/" component={Inicio} />
  <Route path="/distribuidores" component={Distribuidores} />
  <Route path="/plantas" component={Plantas} />
</main>
