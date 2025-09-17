<script>
  let tab = $state("Storyline");  //dandole este valor inicial, siempre vamos a ir a la pagina storyline al recargar
  const paginas = ["Storyline", "Titans"];  //lista

  import Progressbar from '$lib/components/progressbar.svelte'
	import Titans from '$lib/components/titans.svelte';
</script>

<nav class="navbar">
  {#each paginas as p} <!--recorre el array paginas y genera un boton por cada elemento.-->
    <button
      class:p-active={tab === p}  
      onclick={() => tab = p}> <!--aplica la clase p-active solo si el botón corresponde al estado actual-->
      {p} <!--Este es el texto del boton, osea la varialbe p actual-->
    </button>  
  {/each}
</nav>

<div class="content">
  {#if tab === "Storyline"}
  <Progressbar></Progressbar>
  {:else if tab === "Titans"}
    <Titans></Titans>
  {/if}
</div>

<div class= "header">
  <h1>Attack on Titan</h1>
 <!--<p>Poc Svelte - Progress bar & character info</p>-->
</div>


<style>
.navbar{
  position: fixed;
  display: flex;
  gap: 0px;
  background: #353535;
  top:50px;
  left: 0;
  width: 100%;
}

.navbar button{
  font-size: 20px;        
  padding: 10px;   
  border: none;           
  background-color: #353535;
  color: white;            
  cursor: pointer;         /* convierte el mouse en una manito */
  transition: background 0.3s;
}
.header{
  position:fixed;
  display: flex;
  color: white; 
  justify-content: center;
  background-color: #353535;
  top: 0;
  left: 0;
  height: 50px;
  width: 100%;
  font:bolder;
}
.content {
  margin-top:100px; /**Hace que no quede arrbiba del todo el div*/
}

.navbar button:hover{
  background-color: #242424;

}

.navbar button.p-active {
  background-color: #242424;
}

</style>