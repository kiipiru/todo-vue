<script setup lang="ts">
import TodoInput from './entities/todoInput.vue';

</script>

<template>
  <header class="header">
    <h1 class="page_heading">todos</h1>
  </header>
  <main class="todo_list">
    <TodoInput/>
  </main>
</template>

<style>
body {
  height: 100vh;
  width: 100vw;
}

#app {
  background-color: #f5f5f5;
  max-width: 1280px;
  margin: 0px auto;
  height: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  place-items: center;
}

.button {
  background-color: transparent;
  color: #000000;
}

.header {
  width: 100%;
  text-align: center;
}

.page_heading {
  color: #e5d9d9;
  margin: 0px;
  margin-bottom: 8px;
}
.todo_list {
  padding: 12px;
  background-color: #ffffff;
  display: flex;
  flex-direction: column;
  gap: 8px;
}
</style>
