<script lang="ts">
  import { onMount } from 'svelte';
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
  <div class ="titan-card">
  <img src= '/titans/{titan.id}.png' alt={titan.name}/>
    <div class= "descripcion">
    <p>{titan.name}</p>
    </div>
  </div>

{/each}
</div>

<style>
.titanes{
  display:grid;
  grid-template-columns: repeat(auto-fill,minmax(200px, 10px));
  grid-column-gap: 50px;
  grid-row-gap: 60px;
  padding: 40px;
}
.titanes img{
  width: 200px;
  object-fit: cover;
  border-radius: 10px;
}

.titan-card{
  transition: transform 0.2s ease;
}
.descripcion{
  color:white;
  padding: 5px;
  transform: translateY(-15px);
  background-color: #353535;
  border-radius: 5px;


}

.titan-card:hover{
  transform: translateY(-8px);
  cursor:pointer;
}
</style>