<script>
  import { useTracker } from "meteor/rdb:svelte-meteor-data";
  import { Todos } from "../api/todos.js";
  import { LoginWindow, Logout } from "meteor/levelup:svelte-accounts-ui";

  import Todo from "../ui/Todos/Todo.svelte";

  let newTitle = "";
  let newText = "";

  $: todos = useTracker(() => Todos.find({}).fetch());
  $: user = useTracker(() => Meteor.user());
  $: userId = useTracker(() => Meteor.userId());

  function handleSubmit(event) {
    Todos.insert({
      title: newTitle,
      text: newText
    });

    newTitle = "";
    newText = "";
  }
</script>

<style>
  :root {
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
    font-size: 16px;
  }

  form {
    width: 50%;
  }

  input {
    margin: 1rem 0.5rem;
    padding: 1.5rem;
  }

  button {
    padding-top: 15px;
    padding-bottom: 10px;
    margin-top: 25px;
    align-items: center;
  }
</style>

<header>
  <h1>Welcome to my Awesome Todo App</h1>

  {#if $userId}
    <Logout />
  {:else}
    <LoginWindow />
  {/if}

  <form on:submit|preventDefault={handleSubmit}>
    <input type="text" placeholder="Add your Title" bind:value={newTitle} />
    <input type="text" placeholder="Add your Text" bind:value={newText} />

    <button>Submit</button>
  </form>

  {#each $todos as todo}
    <Todo {todo} />
  {/each}
</header>
