<script>
  import { onMount } from "svelte";
  import { useSWR } from "sswr";

  // let users;
  // let isLoading;
  // let error;

  // onMount(fetchData);

  async function fetchData() {
    try {
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/users"
      );

      if (!response.ok) throw new Error(response.statusText);

      users = await response.json();
      console.log(users);
    } catch (err) {
      error = "Sorry, there was an error.";
    }
  }

  async function fetchData2() {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    const users = await response.json();

    if (response.ok) {
      return users;
    } else {
      throw new Error(response.statusText);
    }
  }

  const {
    data: users3,
    error: error3,
    isLoading: isLoading3,
  } = useSWR("https://jsonplaceholder.typicode.com/users");
</script>

<!-- <div>
  {#if users}
    <ul>
      {#each users as user}
        <li>{user.name}</li>
      {/each}
    </ul>
  {:else if error}
    <p>{error}</p>
  {:else}
    <div>Loading...</div>
  {/if}
</div> -->

<!-- <div>
  {#await fetchData2()}
    <div>Loading...</div>
  {:then users}
    <ul>
      {#each users as user}
        <li>{user.name}</li>
      {/each}
    </ul>
  {:catch error}
    <p>Sorry, there was an error.</p>
  {/await}
</div> -->

<div>
  {#if $isLoading3}
    <div>Loading...</div>
  {/if}

  {#if $users3}
    <ul>
      {#each $users3 as user}
        <li>{user.name}</li>
      {/each}
    </ul>
  {/if}

  {#if $error3}
    <div>Error message here</div>
  {/if}
</div>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
