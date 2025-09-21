<script lang="ts">

let progreso = $state(0);
let events: any[] = [
  {checked : false, img:'/shing-attack.webp'},
  {checked : false, img: '/traitors.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
  {checked : false, img: '/eren.png'},
]
  
let completas = $state(0);



  function update() {
    const completed = events.filter(events => events.checked).length;
    progreso = (completed / events.length) * 100;
  }

</script>



<div class = 'progress-bar'>

  <div class ='skeleton'>
      <div class ='fill' style='width: {progreso}%'></div>
      
      {#if progreso === 100}
        <img src='/erenfounder.jpg' alt='eren' style='left: calc({progreso}% - 30px)'>
      {:else}
        <img src='/eren.png' alt='eren' style='left: calc({progreso}% - 30px)'>
      {/if}
  </div>




</div>

<div class="checkboxes">
  {#each events as e}
    <label>
      <input type="checkbox" bind:checked={e.checked} onchange={update}/>
      {#if e.img}
        <img src="{e.img}" alt="event">
      {/if}
    </label>
  {/each}
</div>



<style>
  .progress-bar{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    padding: 15px;
  }
  .skeleton{
    background-color: gray;
    height:40px;
    border-radius: 20px;
    width: 80%;
  }
  .fill{
    background-color: green;
    height:40px;
    border-radius: 20px;
    transition: 0.3s ease;
  }

  .skeleton img{
    top:-55px;
    height:60px;
    position:relative;
    transition: 0.3s ease;
  }

  .checkboxes{
  display:grid;
  grid-template-columns: repeat(auto-fill,minmax(200px, 10px));
  grid-column-gap: 50px;
  grid-row-gap: 60px;
  padding: 100px;
  }

  .checkboxes img{
    height: 80px;

  }
</style>