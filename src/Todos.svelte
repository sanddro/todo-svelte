<script>
  import Todo from "./Todo.svelte";
  import NewTodo from "./NewTodo.svelte";

  const todosFromStorage = JSON.parse(localStorage.getItem("todos"));
  let todos = todosFromStorage || [];

  $: editing = todos.filter(elem => elem.editing).length > 0;

  function updateTodos() {
    todos = [...todos];
    localStorage.setItem("todos", JSON.stringify(todos));
  }

  function onTodoAdded(text) {
    let id = 1;
    if (todos.length) id = todos[todos.length - 1].id + 1;
    todos.push({ text, completed: false, editing: false, id });
    updateTodos();
  }

  function onEditingActivated(todo) {
    todos.forEach(elem => (elem.editing = todo.id === elem.id));
    updateTodos();
  }

  function onEditingDeactivated(todo, value) {
    todo.editing = false;
    todo.text = value;
    updateTodos();
  }

  function onDeleteTodo(todo) {
    todos = todos.filter(elem => elem.id !== todo.id);
    updateTodos();
  }

  function onCheckTodo(todo) {
    todo.completed = !todo.completed;
    updateTodos();
  }
</script>

<style>
  .todos {
    position: relative;
    width: 600px;
    background: white;
    border-radius: 4px;
  }

  .todos:after {
    content: "";
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    pointer-events: none;
    box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2), 0 8px 0 -3px #f6f6f6,
      0 9px 1px -3px rgba(0, 0, 0, 0.2), 0 16px 0 -6px #f6f6f6,
      0 17px 2px -6px rgba(0, 0, 0, 0.2);
  }

  .dark-bg {
    position: fixed;
    width: 100vw;
    height: 100vh;
    left: 0;
    top: 0;
    background: black;
    opacity: 0;
    z-index: -1;
    transition: 0.2s opacity;
  }

  .dark-bg.active {
    opacity: 0.3;
    z-index: 200;
  }
</style>

<div class="todos">
  <NewTodo {onTodoAdded} />
  {#each todos as todo (todo.id)}
    <Todo
      {todo}
      {onEditingActivated}
      {onEditingDeactivated}
      {onDeleteTodo}
      {onCheckTodo} />
  {/each}
  <div class="dark-bg" class:active={editing} />
</div>
