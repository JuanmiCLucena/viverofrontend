<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";

  import Buscar                  from "./Buscar.svelte";
  import Distribuidor                from "./Distribuidor.svelte";
  import Boton                   from "./Boton.svelte";

  const URL = getContext("URL");

  let busqueda = "";
  let distribuidor = {};

  onMount(async () => {
    const response = await fetch(URL.distribuidores);
    const data = await response.json();
    $jsonData = data;
  });

  $: regex = new RegExp(busqueda, "i");
  $: datos = busqueda 
    ? $jsonData.filter(item => regex.test(item.modelo))
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

<h1>Distribuidores</h1>
<Buscar bind:busqueda />

<div class="container">
  <Distribuidor bind:distribuidor>
    <div style="text-align: right">
      <Boton documento={distribuidor} tipo="insertar" coleccion="distribuidores" />
    </div>
  </Distribuidor>
</div>

<div class="container">
  {#each datos as distribuidor}
    <Distribuidor {distribuidor}>
      <div style="text-align: right">
        <Boton documento={distribuidor} tipo="modificar" coleccion="distribuidores" />
        <Boton documento={distribuidor} tipo="eliminar"  coleccion="distribuidores" />
      </div>
    </Distribuidor>
  {/each}
</div>
