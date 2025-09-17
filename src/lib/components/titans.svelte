<script>
  import { onMount } from 'svelte';

  let data = null;
  
  async function getTitans() {
    const response = await fetch('https://api.attackontitanapi.com/titans/1');
    data = await response.json();
    console.log(data);
  }

  onMount(() => {
    getTitans();
  });
</script>
{#if data}
  <h1>{data.name}</h1>
{/if}
