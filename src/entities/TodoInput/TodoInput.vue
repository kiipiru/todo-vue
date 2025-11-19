<script setup lang="ts">
import { ref } from 'vue'
const emit = defineEmits(['input-submitted'])
const isValid = ref<boolean>(true)
const todoText = ref<string>('')
function handleTodoAdd() {
    if (todoText.value && todoText.value.trim()) {
      emit('input-submitted', todoText.value)
      todoText.value = "";
      isValid.value = true;
    } else {
        isValid.value = false;
    }
}
</script>

<template>
     <div
      :class="['input_container', {input_container_invalid: !isValid}]"
      @focusout="isValid = true"
    >
      <button
        :class="['button', 'button_chevron', {button_chevron_invalid: !isValid}]"
        @click="handleTodoAdd"
      ></button>
      <input
        class="input_todo"
        v-model="todoText"
        @keydown='(e) => {
          if (e.key === "Enter") handleTodoAdd();
        }'
        placeholder=""
        aria-labelledby="todo-placeholder"
        :aria-invalid='!isValid'
      />
      <label
        :class="['input_placeholder', {input_placeholder_invalid: !isValid}]"
        id="todo-placeholder"
      >
        What needs to be done?
      </label>
    </div>
</template>

<style>
.button_chevron {
  transition: filter 0.25s;
  background-image: url("../../assets/chevron.svg");
  background-size: 12px 14px;
  background-repeat: no-repeat;
  background-position: center;
  width: 12px;
  height: 14px;
  padding: 6px 0 6px 0;
  justify-self: center;
  align-self: center;
  box-sizing: content-box;
  border: none;
}

.button_chevron_invalid {
  filter: invert(46%) sepia(7%) saturate(1703%) hue-rotate(314deg)
    brightness(103%) contrast(72%);
}

.input_container {
  position: relative;
  transition: 0.25s;
  width: 100%;
  display: flex;
  gap: 4px;
  border: 0.5px solid transparent;
  border-bottom-color: #e6e6e6;
}

.input_container_invalid {
  background-color: #ffebeb;
}

.input_todo {
  color: #4d4d4d;
  background-color: transparent;
  border: none;
  font-size: 20px;
  font-family: inherit;
  width: 100%;
}

.input_placeholder {
  transition: color 0.25s, opacity 0.25s;
  position: absolute;
  z-index: 2;
  color: #e6e6e6;
  font-size: 20px;
  top: 4px;
  left: 19px;
  line-height: 100%;
  opacity: 1;
  pointer-events: none;
}

.input_placeholder_invalid {
  color: #9b7272;
}

.input_todo:not(:placeholder-shown) + .input_placeholder,
.input_todo:focus + .input_placeholder {
  opacity: 0;
}

.input_todo:focus-visible {
  outline: none;
}

</style>