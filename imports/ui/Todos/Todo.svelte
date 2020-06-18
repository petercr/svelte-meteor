<script>
  export let todo;
  import { Todos } from "../../api/todos";
  let updateTitle = todo.title;
  let updateText = todo.text;

  const deleteTodo = () => {
    Todos.remove(todo._id);
  };

  const handleSubmit = event => {
    Todos.update(
      {
        _id: todo._id
      },
      {
        title: updateTitle,
        text: updateText
      }
    );

    updateTitle = "";
    updateText = "";
  };
  // Need to add 2 input fields, 1 for title & text of the Todo
</script>

<style>
  * {
    margin: 10px;
  }

  .title {
    font-weight: 700;
  }
</style>

<!-- Dude this needs some labels and stuff-->
<div>
  <p class="title">{todo.title}:</p>
  <p>{todo.text}</p>
  <button on:click={deleteTodo}>Delete</button>
  <form on:submit|preventDefault={handleSubmit}>
    <input type="text" bind:value={updateTitle} />
    <input type="text" bind:value={updateText} />
    <button>Submit</button>
  </form>
</div>
