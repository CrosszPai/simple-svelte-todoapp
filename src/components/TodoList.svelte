<script>
  import Todo from "./Todo.svelte";
  export let todos;
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  const toggleDone = ({ detail: id }) => {
    dispatch("toggleDone", id);
  };
  const removeTodo = ({ detail: id }) => {
    dispatch("removeTodo", id);
  };
</script>

<ul>
  {#each todos as todo}
    <Todo
      {todo}
      on:toggleDone={toggleDone}
      on:removeTodo={removeTodo} />
  {/each}
</ul>
