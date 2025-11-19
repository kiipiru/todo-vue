<script setup lang="ts">
const props = defineProps<{ todo: todo }>();
const emit = defineEmits(["todo-status-changed"]);
</script>

<template>
    <div class="todo_item_container">
        <button class="button button_todo" :class="{ button_todo_done: props.todo.isDone }"
            @click="emit('todo-status-changed', props.todo)"></button>
        <p class="todo_item_name" :class="{ todo_item_name_done: props.todo.isDone }">
            {{ props.todo.text }}
        </p>
    </div>
</template>

<style>
.todo_item_container {
    width: 100%;
    display: flex;
    flex-direction: row;
    border-bottom: 0.5px solid #e6e6e6;
    gap: 4px;
    align-items: center;
}

.button_todo {
    box-sizing: content-box;
    border: 1.5px solid #f2f2f2;
    border-radius: 50%;
    height: 13.5px;
    min-width: 13.5px;
    padding: 0;
}

.button_todo:hover:not(.button_todo_done) {
    border-color: #ddd;
}

.button_todo_done {
    border-color: transparent;
    background-image: url("../../assets/todoChecked.svg");
    background-size: 17px 17px;
    background-position: center;
}

.todo_item_name {
    margin: 0;
    color: #4d4d4d;
    font-size: 20px;
    transition: 0.25s ease;
    text-align: start;
    overflow-wrap: break-word;
    overflow: hidden;
    height: 100%;
    padding: 4px 0px;
}

.todo_item_name_done {
    text-decoration: line-through;
    color: #e6e6e6;
}
</style>
