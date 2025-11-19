<script setup lang="ts">
import { computed, ref } from "vue";
import TodoInput from "./entities/TodoInput/TodoInput.vue";
import TodoItem from "./entities/TodoItem/TodoItem.vue";
import FilterButton from "./entities/FilterButton/FilterButton.vue";
import "./fonts.css";
import type { filter, todo } from "./types/types";
let key = 1;
const todos = ref<todo[]>([]);
const filters = ref<filter[]>(["all", "active", "completed"]);
const selectedFilter = ref<filter>("all");
const leftTodosCount = computed(() => {
  let count = 0;
  for (let t of todos.value) {
    if (t.isDone === false) count++;
  }
  return count;
});
const visibleTodos = computed(() => {
  if (selectedFilter.value === 'all') return todos.value
  if (selectedFilter.value === 'active') return todos.value.filter((t) => t.isDone === false)
  if (selectedFilter.value === 'completed') return todos.value.filter((t) => t.isDone === true)
  return []
 })

function addTodo(todoText: string) {
  todos.value.push({ key: key++, text: todoText, isDone: false });
}
function toggleTodo(t: todo) {
  t.isDone = !t.isDone
}
function clearCompleted() {
  todos.value = todos.value.filter((t) => t.isDone === false)
}
</script>

<template>
  <header class="header">
    <h1 class="page_heading">todos</h1>
  </header>
  <main class="todo_list">
    <TodoInput @inputSubmitted="addTodo" />
    <TodoItem
      v-for="todo in visibleTodos"
      :key="todo.key"
      v-on:todo-status-changed="toggleTodo"
      :todo="todo"
    >
    </TodoItem>
    <div class="todo_params_bar">
      <p class="items_left_text">
        {{ leftTodosCount }} item{{ leftTodosCount !== 1 ? "s" : "" }} left
      </p>
      <div class="filters_container">
        <FilterButton
          v-for="filter in filters"
          :title="filter"
          :isActive="filter === selectedFilter"
          v-on:filter-selected="(f: filter) => selectedFilter = f"
        ></FilterButton>
      </div>
      <button :disabled="!todos.some(t => t.isDone)" class="button button_clear" @click="clearCompleted">
        Clear completed
      </button>
    </div>
  </main>
</template>

<style>
body {
  height: 100vh;
  width: 100vw;
  box-sizing: border-box;
  margin: 0px;
  font-weight: 100;
  font-family: 'SF Compact', sans-serif;
}

#app {
  max-width: 1600px;
  margin: 0px auto;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #f5f5f5;
  color: #4d4d4d;
}

.button {
  background-color: transparent;
  color: inherit;
  font-family: 'SF Compact', sans-serif;
  font-weight: inherit;
  font-size: 12px;
}

.header {
  width: 100%;
  text-align: center;
}

.page_heading {
  color: #e5d9d9;
  margin: 0px 0px 8px 0px;
  font-size: 3.2em;
  font-weight: 100;
}

.todo_list {
  padding: 12px;
  background-color: #ffffff;
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.todo_params_bar {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 40px;
}

.filters_container {
  display: flex;
  max-width: 136px;
  gap: 12px;
  padding: 0px;
}

.items_left_text {
  padding-top: 2px;
  font-size: 12px;
  margin: 0px;
  min-width: 55px;
}

.button_clear {
  font-size: 12px;
  line-height: 100%;
  letter-spacing: 0%;
  padding: 0;
  border: none;
}

.button_clear:hover {
  color: #666;
  transition: color 0.25s;
}

</style>
