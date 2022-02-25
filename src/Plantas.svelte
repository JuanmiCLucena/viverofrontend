<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";

  import Buscar                  from "./Buscar.svelte";
  import Planta                from "./Planta.svelte";
  import Boton                   from "./Boton.svelte";

  const URL = getContext("URL");

  let busqueda = "";
  let planta = {};

  onMount(async () => {
    const response = await fetch(URL.plantas);
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

<h1>Plantas</h1>
<Buscar bind:busqueda />

<div class="container">
  <Planta bind:planta>
    <div style="text-align: right">
      <Boton documento={planta} tipo="insertar" coleccion="plantas" />
    </div>
  </Planta>
</div>

<div class="container">
  {#each datos as planta}
    <Planta {planta}>
      <div style="text-align: right">
        <Boton documento={planta} tipo="modificar" coleccion="plantas" />
        <Boton documento={planta} tipo="eliminar"  coleccion="plantas" />
      </div>
    </Planta>
  {/each}
</div>