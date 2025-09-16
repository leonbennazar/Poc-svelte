<script lang="ts">
  import { onMount } from 'svelte';

  let activeTab = 'News';

  const tabs = [
    { name: 'Home', color: 'red', content: 'Home is where the heart is..' },
    { name: 'News', color: 'green', content: 'Some news this fine day!' },
    { name: 'Contact', color: 'blue', content: 'Get in touch, or swing by for a cup of coffee.' },
    { name: 'About', color: 'orange', content: 'Who we are and what we do.' }
  ];

  function openPage(tabName: string) {
    activeTab = tabName;
  }

  onMount(() => {
    activeTab = 'News';
  });
</script>

<style>
* {box-sizing: border-box}
body, html {
  height: 100%;
  margin: 0;
  font-family: Arial;
}
.tablink {
  background-color: #555;
  color: white;
  float: left;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 14px 16px;
  font-size: 17px;
  width: 25%;
}
.tablink:hover {
  background-color: #777;
}
.tabcontent {
  color: white;
  display: none;
  padding: 100px 20px;
  height: 100%;
}
.tabcontent.active {
  display: block;
}
#Home {background-color: red;}
#News {background-color: green;}
#Contact {background-color: blue;}
#About {background-color: orange;}
</style>

<div>
  {#each tabs as tab}
    <button
      class="tablink"
      style="background-color: {activeTab === tab.name ? tab.color : ''}"
      on:click={() => openPage(tab.name)}
      id={tab.name === 'News' ? 'defaultOpen' : undefined}
    >
      {tab.name}
    </button>
  {/each}
</div>

{#each tabs as tab}
  <div
    id={tab.name}
    class="tabcontent {activeTab === tab.name ? 'active' : ''}"
    style="background-color: {tab.color};"
  >
    <h3>{tab.name}</h3>
    <p>{tab.content}</p>
  </div>
{/each}
