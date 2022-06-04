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
  {#each items as item}
    <div>
      <p>Title: {item.title}</p>
      <p>Category: {item.category}</p>
      <p>Description: {item.description}</p>
    </div>
    <hr>
  {:else}
    <!-- this block renders when Tasks are empty OR items.length === 0 -->
    <p>loading...</p>
  {/each}
</main>