<script>
  export let onTodoAdded;

  let value = '';

  function onKeyUp(event) {
    if (event.key !== 'Enter') return;
    onTodoAdded(value.trim());
    value = '';
  }
</script>

<div>
  <input
    type="text"
    placeholder="What needs to be done?"
    class="new-todo-input"
    bind:value
    on:keyup="{event => onKeyUp(event)}"
  />
</div>

<style>
  .new-todo-input {
    width: 100%;
    font-size: 24px;
    border: none;
    padding: 24px 14px 24px 50px;
    background: transparent;
  }

  .new-todo-input:focus {
    outline: none;
  }

  .new-todo-input::placeholder {
    opacity: 0.5;
  }
</style>
