<script>
  let tab = $state("Home");  //dandole este valor inicial, siempre vamos a ir a la pagina storyline al recargar
  const paginas = ["Home", "Storyline", "Titans"];  //lista

  import Progressbar from '$lib/components/progressbar.svelte'
	import Titans from '$lib/components/titans.svelte';
  import Home from '$lib/components/home.svelte'
</script>



<div class="content">
  {#if tab === "Home"}
  <Home></Home>
  {:else if tab === "Storyline"}
  <Progressbar></Progressbar>
  {:else if tab === "Titans"}
    <Titans></Titans>
  {/if}
</div>


<div class= "header">
  <h1>Attack on Svelte</h1>
 <!--<p>Poc Svelte - Progress bar & character info</p>-->
</div>



<nav class="navbar">
  {#each paginas as p} <!--recorre el array paginas y genera un boton por cada elemento.-->
    <button
      class:p-active={tab === p}  
      onclick={() => tab = p}> <!--aplica la clase p-active solo si el botón corresponde al estado actual-->
      {p} <!--Este es el texto del boton, osea la varialbe p actual-->
    </button>  
  {/each}
</nav>



<style>
.navbar{
  position: fixed;
  display: flex;
  background: #e53935;
  top:50px;
  left: 0;
  width: 100%;
}

.navbar button{
  font-size: 20px;        
  padding: 10px;   
  border: none;           
  background-color: #e53935;
  color: white;                  
  transition: background 0.3s;
}
.header{
  position:fixed;
  display: flex;
  color: white; 
  justify-content: center;
  background-color: #e53935;
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
  background-color: #b71c1c;
    cursor: pointer; 

}

.navbar button.p-active {
  background-color: #b71c1c;
}

</style>