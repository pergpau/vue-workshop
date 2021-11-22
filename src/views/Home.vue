<template>
  <h1 class="title">Gjøremål</h1>
  <div class="input-container">
    <input placeholder="Hva må du gjøre?" />
    <button>Legg til</button>
  </div>

  <div class="todos-container">
    <div class="todo-item">
      <label class="todo-checkbox">
        <input
          type="checkbox"
        >
        <span></span>
      </label>
      <div>Et gjøremål</div>
      <span
        class="material-icons"
      >
        delete
      </span>
    </div>

  </div>
</template>

<script>

export default {
  name: 'Home'
}
</script>
