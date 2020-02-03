<script>
  export let todo;
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  function handleCheckbox() {
    dispatch("toggleDone", todo.id);
  }

  function handleRemove() {
    dispatch("removeTodo", todo.id);
  }
</script>

<style>
  .item-container {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
    width: 437px;
    margin-left: -27px;
  }

  .wrapper {
    flex-wrap: wrap;
    display: flex;
    align-items: center;
    width: 82%;
  }

  .checkbox {
    margin: 0;
    width: 30px;
    height: 30px;
  }

  li {
    transition: 0.5s;
  }

  .li-notdone {
    margin: 0.7em;
    list-style: none;
    font-size: 1.2em;
  }

  .li-done {
    color: #bbb;
    margin: 0.7em;
    list-style: none;
    font-size: 1.2em;
  }

  .line {
    position: absolute;
    margin: 0 40px;
    width: 280px;
    border-bottom: 1px solid #bbb;
  }

  .del {
    flex-wrap: wrap;
    background: crimson;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 95px;
    height: 40px;
  }

  .del:hover {
    background: crimson;
    transform: rotate(5deg) scale(1.1);
  }
</style>

<div class="item-container">
  <div class="wrapper">
    <input
      class="checkbox"
      type="checkbox"
      on:click={handleCheckbox}
      defaultChecked={todo.done} />
    <div class:line={todo.done} />
    <li class={todo.done ? 'li-done' : 'li-notdone'}>{todo.task}</li>
  </div>
  <button class="del" on:click={handleRemove}>x</button>
</div>
