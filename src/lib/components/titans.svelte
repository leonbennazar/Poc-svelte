<script lang="ts">
  import { onMount } from 'svelte';
  import {goto} from '$app/navigation';
  let mostrar: any= 0
  let data: any[] = [];  //en typescript: data va a ser un array de cualquier tipo

  async function getTitans() {
    const req = await fetch('https://api.attackontitanapi.com/titans/');
    const res = await req.json();
    data = res.results;  //uso esto porque la request devuelve objetos
    console.log(data); //si la consola devuelve entre {}, es objeto, entre [] es array
  }

  onMount(() => {
    getTitans();
  });
</script>



  <div class="titanes"> 
  {#each data as titan}
  <button class="accionTitan" on:click={() => mostrar = titan.id}>
    <div class ="titan-card">
      <img src= '/titans/{titan.id}.png' alt={titan.name}/>
        <div class= "descripcion">
        <p>{titan.name}</p>
      </div>
    </div>
  </button>
  {/each}
  </div>

  {#each data as titan}    <!--Esto detecta que titan se tocó, para mostrar el popup-->
  {#if mostrar === titan.id}
    <div class="overlay">
      <div class="popup" >
        <h1>{titan.name}</h1>
      <img src='/titans/{titan.id}.png' alt={titan.name} />
        <p>● Habilities:{titan.abilities}<br>
        ● Height: {titan.height}<br>
        ● Loyal to {titan.allegiance}</p>
        <button on:click={() => mostrar = 0}>Close</button>
      </div>
    </div>
  {/if}
  {/each}




<style>
.titanes{
  display:grid;
  grid-template-columns: repeat(auto-fill,minmax(200px, 10px));
  grid-column-gap: 50px;
  grid-row-gap: 60px;
  padding: 100px;
}
.titanes img{
  width: 200px;
  object-fit: cover;
  border-radius: 10px;
}

.titanes button{
  background: none;
  border: none;
}

.titan-card{
  transition: 0.2s ease;
}
.descripcion{
  color:white;
  padding: 5px;
  width: 190px;
  transform: translateY(-15px);
  background-color: #d32f2f;
  border-radius: 5px;
  border-top-left-radius: 0px ;
  border-top-right-radius:0px;

}

.titan-card:hover{
  transform: translateY(-8px);
  cursor:pointer;
}
  .overlay { /*El fondo del popup y ademas lo que lo centra*/
    position:fixed;
    display:flex;
    align-items: center;
    justify-content: center;
    top: 0;
    left: 0;
    width:100%;
    height: 100%;
    background: #111111b4
  }

  .popup {
    background: #3f0101;
    color: #fff;  
    border-radius: 15px;
    width: 500px;
    text-align: center;
    box-shadow: 0 0 10px #000;
    font-weight:bold;
  }
  .popup img{
    margin-top: 40px;
    width:300;
    height:300px;
  }
  .popup h1{
    margin-bottom: -20px;
  }
 .popup p{ 
  margin-bottom: -5px;
  text-align:left;
  padding: 15px;
  color:#cfcfcf;
 }
 .popup button{
  margin-bottom: 10px;
  cursor:pointer;
 }


</style>