<template>
  <transition-group name="list" tag="ul" class="space-y-2">
    <li
      v-for="(task, index) in props.tasks"
      :key="task.id"
      class="flex items-start gap-2 bg-white dark:bg-gray-800 border border-gray-100 dark:border-gray-700 rounded px-3 py-2 shadow-sm text-gray-800 dark:text-gray-100 text-base"
      :class="{
        'line-through text-orange-400 dark:text-orange-300': task.done,
      }"
      :data-id="task.id"
    >
      <span class="text-xs text-gray-400 dark:text-gray-300 mt-1">{{
        index + 1
      }}</span>
      <span
        class="flex-1 break-words whitespace-pre-line min-w-0 dark:text-gray-100"
        >{{ task.title }}</span
      >
      <label
        class="flex items-center gap-2 text-sm text-gray-600 dark:text-gray-200 select-none"
      >
        <small>Done</small>
        <input
          type="checkbox"
          @input="emits('toggleDone', task.id)"
          :checked="task.done"
          class="accent-blue-500 dark:accent-blue-400 w-4 h-4 rounded border-gray-300 dark:border-gray-600 focus:ring-2 focus:ring-blue-400 transition"
        />
      </label>
      <button
        class="ml-2 px-2 py-1 rounded bg-red-100 dark:bg-red-900 text-red-600 dark:text-red-200 hover:bg-red-200 dark:hover:bg-red-800 transition text-xs font-semibold"
        @click="emits('removeTask', task.id)"
        title="Remove task"
        type="button"
      >
        Remove
      </button>
    </li>
  </transition-group>
</template>

<script lang="ts" setup>
import type { Task } from "../../types";
const props = defineProps<{ tasks: Task[] }>();

const emits = defineEmits<{
  toggleDone: [id: string];
  removeTask: [id: string];
}>();
</script>

<style>
/* Ensure Tailwind dark mode is set to 'class' in tailwind.config.js */
</style>
