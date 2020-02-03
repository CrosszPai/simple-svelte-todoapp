<script>
  import uuid from "uuid";
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  let todo = {
    id: "",
    task: "",
    done: false
  };

  function handleInputChange(e) {
    todo = { ...todo, task: e.target.value };
  }

  function handleSubmit(e) {
    e.preventDefault();
    if (todo.task.trim()) {
      dispatch("addTodo", { ...todo, id: uuid.v4() });
      todo = { ...todo, task: "" };
    }
  }
</script>

<style>
  form {
    flex-wrap: wrap;
    display: flex;
    justify-content: center;
    width: 100%;
  }

  input {
    width: 300px;
    margin: 0 1em;
    padding: 1em;
    font-family: inherit;
    border: 1px solid #555;
    border-radius: 0;
  }

  button {
    color: white;
    background: #333;
    padding: 0 2em;
    font-family: inherit;
    font-weight: 400;
    font-size: 1em;
    border: none;
    transition: 0.3s;
  }

  button:hover {
    background: var(--main-color);
    cursor: pointer;
  }
</style>

<form on:submit={handleSubmit}>
  <input
    name="task"
    type="text"
    bind:value={todo.task}
    on:change={handleInputChange} />
  <button type="submit">ADD</button>
</form>

