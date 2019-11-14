<script>
  import { todos } from "./store.js";
  import { faTrash } from "@fortawesome/free-solid-svg-icons/faTrash";
  import Icon from "fa-svelte";

  function handleKeyDown(event) {
    if (event.which === 13) {
      const text = event.target.value;
      if (!text) {
        return;
      }
      todos.update(n => [...n, { description: text, completed: false }]);
    }
  }
  function removeTask(index) {
    todos.update(t => [...t.slice(0, index), ...t.slice(index + 1, t.length)]);
  }
  function toggleComplete(index, todo) {
    todo.completed = !todo.completed;
    todos.update(t => [
      ...t.slice(0, index),
      todo,
      ...t.slice(index + 1, t.length)
    ]);
  }
</script>

<style>
  h1 {
    color: silver;
  }
  .heading {
    display: flex;
    flex-direction: column;
  }
  .sub-heading {
    display: flex;
    margin: 10px;
    justify-content: center;
  }
  input[type="text"] {
    width: 100%;
  }
  input[type="checkbox"] {
    margin-right: 10px;
    margin-top: 8px;
  }
  .lower-part {
    display: flex;
    flex-direction: column;
    background-color: #bbb;
    max-width: 500px;
    margin: auto;
    border-bottom: 1px solid white;
  }
  .todo-block {
    display: flex;
    flex-direction: column;
    margin: 5px;
  }
  .todo {
    display: flex;
    width: 100%;
  }
  .div2 {
    flex: 2;
  }
  .div3 {
    margin-left: 10px;
  }
  .div3 span {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  div :global(.delete) {
    color: #fff;
    margin-top: 5px;
  }
  .action-box {
    background-color: #bbb;
    max-width: 500px;
    margin: auto;
    border-bottom: 1px solid white;
  }
  .action-box div {
    padding-top: 4px;
    display: flex;
    justify-content: space-around;
  }
  .last-box1 {
    background-color: #bbb;
    max-width: 490px;
    height: 3px;
    margin: auto;
  }
  .last-box2 {
    background-color: #bbb;
    max-width: 480px;
    height: 3px;
    margin: auto;
  }
  .last-box3 {
    background-color: #bbb;
    max-width: 470px;
    height: 3px;
    margin: auto;
  }
</style>

<div>
  <div class="heading">
    <div class="sub-heading">
      <h1>Todo Using Svelte</h1>
    </div>
  </div>
  <div class="lower-part">
    <div class="sub-heading">
      <input
        type="text"
        placeholder="Enter New Task"
        on:keydown={handleKeyDown} />
    </div>
    <div class="todo-block">
      {#each $todos as todo, i}
        <div class="todo">
          <div class="div1">
            <input
              on:click={() => toggleComplete(i, todo)}
              type="checkbox"
              checked={todo.completed} />
          </div>
          <div class="div2">
            <input class="task" type="text" value={todo.description} />
          </div>
          <div class="div3">
            <span on:click={() => removeTask(i)}>
              <Icon class="delete" icon={faTrash} />
            </span>
          </div>

        </div>
      {/each}
    </div>
  </div>
  <div class="action-box">
    <div>
      <div>
        <button type="button">All</button>
      </div>
      <div>
        <button type="button">Pending</button>
      </div>
      <div>
        <button type="button">Completed</button>
      </div>
    </div>
  </div>
  <div class="last-box1" />
  <div class="last-box2" />
  <div class="last-box3" />
</div>
