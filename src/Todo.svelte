<script>
  export let todo,
    onEditingActivated,
    onEditingDeactivated,
    onDeleteTodo,
    onCheckTodo;
</script>

<div
  class="todo"
  class:completed="{todo.completed}"
  class:editing="{todo.editing}"
>
  <div class="todo-checkbox">
    <input
      type="checkbox"
      checked="{todo.completed}"
      on:change="{() => onCheckTodo(todo)}"
    />
    <label></label>
  </div>
  <div
    type="text"
    class="edit-todo-input"
    tabindex="0"
    on:dblclick="{() => onEditingActivated(todo)}"
    on:blur="{event => onEditingDeactivated(todo, event.target.innerHTML.trim())}"
    on:keyup="{event => {
      if (event.key === 'Escape') event.target.blur();
    }}"
    contenteditable="{todo.editing}"
  >
    {@html todo.text}
  </div>
  <div class="delete-button-wrapper">
    <button class="delete-button" on:click="{() => onDeleteTodo(todo)}">
      <span>✖</span>
    </button>
  </div>
</div>

<style>
  .todo {
    display: flex;
    align-items: center;
    word-break: break-all;
    border-top: 1px solid #dededf;
    padding: 0 14px;
  }

  .todo.editing .todo-checkbox,
  .todo.editing .delete-button-wrapper {
    visibility: hidden;
  }

  .todo .delete-button-wrapper {
    margin-left: 10px;
    flex: 1;
    text-align: right;
  }

  .todo .delete-button {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    background: red;
    color: white;
    font-size: 14px;
    font-weight: bold;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0;
    cursor: pointer;
    transition: 0.1s all;
  }

  .todo .delete-button {
    opacity: 0;
    transition: 0.1s opacity;
  }

  .todo:hover .delete-button {
    opacity: 0.5;
  }

  .todo .delete-button:hover {
    opacity: 0.7;
  }

  .edit-todo-input {
    width: 100%;
    border: none;
    padding: 18px 10px;
    font-size: 20px;
    margin-left: 20px;
    resize: none;
    background: white;
  }

  .edit-todo-input:focus {
    outline: none;
  }

  .todo.editing .edit-todo-input {
    outline: none;
    box-shadow: 0 0 5px -1px rgba(0, 0, 0, 0.7);
    z-index: 500;
  }

  .todo.completed .edit-todo-input {
    text-decoration: line-through;
    color: #999;
  }
</style>
