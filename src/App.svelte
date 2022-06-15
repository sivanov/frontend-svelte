<style>
  .card {
    background-color: dodgerblue;
    color: white;
    padding: 1rem;
  }
  .cards {
    margin: 0 auto;
    display: grid;
    gap: 1rem;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  }
</style>

<script>
  import { onMount } from "svelte";
  // url addres to API
  const endpoint = "http://127.0.0.1:8000/api/v1/todos/";
  // hld all results from API like JSON Data
  let items = [];

  onMount(async () => {
    const responce = await fetch(endpoint);
    const data = await responce.json();
    // result can be seen in browser console
    console.log("API data: ", data);
    items = data;
  });
</script>

<main>
  <h3>TODO App</h3>
  <div class="cards">
    {#each items as item}
        <div class="card">
          <h4>{item.title}</h4>
          <p><i>Category: {item.category}</i></p>
          <p>Description: {item.description}</p>
        </div>
    {:else}
      <!-- this block renders when Tasks are empty OR items.length === 0 -->
      <div class="card">
        <p>loading...</p>
      </div>
    {/each}
  </div> 
</main>