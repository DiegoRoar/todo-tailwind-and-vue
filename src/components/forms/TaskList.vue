<template>
  <ul class="space-y-2">
    <li
      v-for="(task, index) in tasks"
      :key="task.id"
      class="flex items-center gap-3 bg-white border border-gray-100 rounded-lg px-4 py-3 shadow-sm hover:shadow-md transition text-gray-800 text-base group"
    >
      <span class="text-xs text-gray-400 mt-1">{{ index + 1 }}</span>
      <span
        :class="
          ['flex-1 break-words whitespace-pre-line min-w-0 transition'],
          task.done ? 'line-through text-gray-400' : ''
        "
      >
        {{ task.title }}
      </span>
      <label class="flex items-center gap-2 text-sm text-gray-600 select-none">
        <input
          type="checkbox"
          class="accent-blue-500 w-4 h-4 rounded border-gray-300 focus:ring-2 focus:ring-blue-400 transition"
          @input="emits('toggleDone', task.id)"
          :checked="task.done"
        />
        <span class="hidden sm:inline">Done</span>
      </label>
      <button
        class="ml-2 px-2 py-1 rounded-lg bg-red-50 text-red-500 border border-red-200 hover:bg-red-100 hover:text-red-700 transition text-xs font-semibold shadow-sm group-hover:scale-105 flex items-center justify-center"
        @click="emits('removeTask', task.id)"
        title="Remove task"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-4 w-4"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M6 18L18 6M6 6l12 12"
          />
        </svg>
      </button>
    </li>
  </ul>
</template>

<script lang="ts" setup>
import type { Task } from "../../types";
const { tasks } = defineProps<{ tasks: Task[] }>();

const emits = defineEmits<{
  toggleDone: [id: string];
  removeTask: [id: string];
}>();
</script>

<style scoped></style>
