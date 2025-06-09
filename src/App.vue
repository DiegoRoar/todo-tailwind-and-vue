<template>
  <main
    class="w-full h-screen bg-gradient-to-br from-blue-100 via-purple-100 to-pink-100"
  >
    <div
      class="w-full sm:w-[95%] mx-auto h-screen bg-gray-50 shadow-2xl shadow-gray-400/60 border border-gray-200"
    >
      <h1 class="title-h1 text-[min(4.5vw,35px)] text-center my-2">
        {{ title }}
      </h1>
      <FormTasks @add-task="addTask" />

      <p>{{ tasks.length }}</p>
      <p v-for="task in tasks" :key="task.id" class="text-black text-lg">
        {{ task.title }}
      </p>
    </div>
  </main>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import FormTasks from "./components/forms/FormTasks.vue";
import type { Task } from "./types";

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
