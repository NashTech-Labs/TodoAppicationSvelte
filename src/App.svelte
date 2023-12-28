<script>
  export let todos = [];

  let newTodo = "";

  function addTodo() {
    if (newTodo.trim() !== "") {
      todos = [...todos, { id: Date.now(), text: newTodo, completed: false }];
      newTodo = "";
    }
  }

  function removeTodo(id) {
    todos = todos.filter(todo => todo.id !== id);
  }

  function toggleTodo(id) {
    todos = todos.map(todo =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    );
  }
</script>

<style>
  main {
    text-align: center;
    max-width: 400px;
    margin: auto;
    padding: 20px;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: flex;
    align-items: center;
    margin-bottom: 8px;
  }

  input[type="checkbox"] {
    margin-right: 8px;
  }

  span.completed {
    text-decoration: line-through;
    color: #888;
  }
</style>

<main>
  <h1>Todo List</h1>

  <div>
    <input bind:value={newTodo} placeholder="Add a new todo" />
    <button on:click={addTodo}>Add</button>
  </div>

  <ul>
    {#each todos as { id, text, completed }}
      <li>
        <input type="checkbox" bind:checked={completed} />
        <span class:completed={completed} style="margin-right:8px">{text}</span>
        <button on:click={() => removeTodo(id)}>Remove</button>
      </li>
    {/each}
  </ul>
</main>


