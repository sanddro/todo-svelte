<script>
  import Todos from './Todos.svelte';
  let name = '';
</script>

<div class="hint">
  Enter to add
  <br />
  Double click to edit
</div>

<main>
  <Todos />
</main>

<style>
  .hint {
    position: fixed;
    top: 20px;
    left: 20px;
    color: #ddd;
    font-size: 14px;
  }

  main {
    display: flex;
    justify-content: center;
    padding: 100px 0;
  }
</style>
