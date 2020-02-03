<script>
  import TodoForm from "./components/TodoForm.svelte";
  import TodoList from "./components/TodoList.svelte";
  import { onMount } from "svelte";
  const LOCAL_STORAGE_KEY = "react-todo-list-todos";

  let todos = [];
  let loading = false;
  onMount(() => {
    const storageTodos = JSON.parse(localStorage.getItem(LOCAL_STORAGE_KEY));
    if (storageTodos) {
      todos = storageTodos;
	}
	loading = true;
  });

  $:if(loading) {
    console.log(todos, "todos change");
    localStorage.setItem(LOCAL_STORAGE_KEY, JSON.stringify(todos));
  }
  function addTodo({ detail: todo }) {
    todos = [...todos, todo];
  }

  function toggleDone({ detail: id }) {
    todos = todos.map(todo => {
      if (todo.id ===  id ) {
        return {
          ...todo,
          done: !todo.done
        };
      }
      return todo;
    });
  }

  function removeTodo({ detail: id }) {
	console.log(id)
    todos = todos.filter(todo => todo.id !== id);
  }
</script>

<style>
  @import url("https://fonts.googleapis.com/css?family=Poppins:300,400&display=swap");

  :root {
    --main-color: #00ccff;
  }

  .App {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    font-family: "Poppins", sans-serif;
    font-weight: 300;
  }

  strong {
    color: var(--main-color);
    font-weight: 400;
  }

  header {
    font-size: 4em;
    margin: 1em;
  }
</style>

<div class="App">
  <header>
    S I M P L E
    <strong>T O D O</strong>
  </header>
  <TodoForm on:addTodo={addTodo} />
  <TodoList {todos} on:toggleDone={toggleDone} on:removeTodo={removeTodo} />
</div>
