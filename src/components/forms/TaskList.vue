<template>
  <ul class="space-y-2">
    <li
      v-for="(task, index) in props.tasks"
      :key="task.id"
      class="flex items-center gap-2 bg-white border border-gray-100 rounded px-3 py-2 shadow-sm text-gray-800 text-base"
    >
      <span class="text-xs text-gray-400">{{ index + 1 }}</span>
      <span class="flex-1 truncate">{{ task.title }}</span>
      <label class="flex items-center gap-2 text-sm text-gray-600">
        <small>Done</small>
        <input
          type="checkbox"
          @input="emits('toggleDone', task.id)"
          :checked="task.done"
        />
      </label>
    </li>
  </ul>
</template>

<script lang="ts" setup>
import type { Task } from "../../types";
const props = defineProps<{ tasks: Task[] }>();

const emits = defineEmits<{
  toggleDone: [id: string];
}>();
</script>

<style scoped></style>
