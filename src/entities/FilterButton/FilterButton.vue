<script setup lang="ts">
import type { filter } from '@/types/types';

const props = defineProps<{title: filter, isActive: boolean}>()
const emit = defineEmits(['filter-selected'])
</script>

<template>
    <button
      :disabled="isActive"
      @click="emit('filter-selected', props.title)"
      class="button button_filter"
      :class="{button_selected: isActive}"
    >
      {{props.title}}
    </button>
</template>

<style>

.button_filter {
  border: none;
  text-transform:capitalize;
}

.button_filter:hover {
  color: #666;
  transition: color 0.25s ease;
}

.button_selected {
  border: 0.5px solid #e7d9d9;
  border-radius: 0%;
}

</style>