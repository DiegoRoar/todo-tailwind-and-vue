<template>
  <main
    class="min-h-screen flex items-center justify-center bg-gradient-to-br from-blue-100 via-purple-100 to-pink-100"
  >
    <div
      class="w-full max-w-xl mx-auto min-h-screen md:min-h-[60vh] bg-white/95 shadow-xl border border-gray-100 rounded-lg flex flex-col items-center p-4"
    >
      <h1 class="title-h1 text-[min(6vw,28px)] text-center my-6 tracking-tight">
        {{ title }}
      </h1>
      <FormTasks @add-task="addTask" />
      <div class="w-full mt-6">
        <div
          v-if="tasks.length < 1"
          class="text-gray-400 text-center text-base italic py-8"
        >
          Add a task to get started...
        </div>
        <TaskList :tasks="tasks" />
      </div>
    </div>
  </main>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import FormTasks from "./components/forms/FormTasks.vue";
import type { Task } from "./types";
import TaskList from "./components/forms/TaskList.vue";

const title = "Task App Manager";
const tasks = ref<Task[]>([]);
const addTask = (newTask: string) => {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false,
  });
};
</script>

<style scoped></style>
