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
  <h1>{titan.name} {titan.img}</h1>
  <img src= '/titans/{titan.id}.png' alt={titan.name}>
{/each}
</div>

<style>
.titanes img{
  width: 500px;
}
</style>