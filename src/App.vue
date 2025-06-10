<template>
  <main
    :class="[
      'min-h-screen flex items-center justify-center transition-colors duration-300',
      isDark
        ? 'bg-gradient-to-br from-gray-900 via-gray-800 to-gray-700'
        : 'bg-gradient-to-br from-blue-100 via-purple-100 to-pink-100',
    ]"
  >
    <div
      :class="[
        'w-full max-w-2xl mx-auto min-h-screen md:min-h-[60vh] shadow-xl border rounded-lg flex flex-col items-center p-4 transition-colors duration-300',
        isDark
          ? 'bg-gray-900 border-gray-700 text-gray-100'
          : 'bg-white/95 border-gray-100 text-gray-900',
      ]"
    >
      <div class="w-full flex justify-end mb-2">
        <button
          class="btn-primary px-3 py-1 text-xs rounded transition dark:bg-gray-900 dark:text-gray-100 dark:hover:bg-gray-800"
          @click="toggleDarkMode"
        >
          {{ isDark ? "Light Mode" : "Dark Mode" }}
        </button>
      </div>
      <h1 class="title-h1 text-[min(6vw,28px)] text-center my-4 tracking-tight">
        {{ title }}
      </h1>
      <FormTasks @add-task="addTask" />
      <div class="w-full mt-6">
        <p
          v-if="tasks.length < 1"
          class="p-default text-center text-base italic py-8 transition-colors duration-300"
        >
          Add a task to get started...
        </p>
        <p v-else class="p-default">
          {{ totalDone }} / {{ tasks.length }} tasks completed
        </p>
        <TaskList
          :tasks="tasks"
          @toggle-done="toggleDone"
          @remove-task="removeTask"
        />
      </div>
    </div>
  </main>
</template>

<script lang="ts" setup>
import { onMounted, ref, computed } from "vue";
import FormTasks from "./components/forms/FormTasks.vue";
import type { Task } from "./types";
import TaskList from "./components/forms/TaskList.vue";

const title = "Task App Manager";
const tasks = ref<Task[]>([]);
const isDark = ref(false);

const addTask = (newTask: string) => {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false,
  });
};

const toggleDone = (id: string) => {
  const task = tasks.value.find((task) => task.id === id);
  if (task) {
    task.done = !task.done;
  }
};

const removeTask = (id: string) => {
  tasks.value = tasks.value.filter((task) => task.id !== id);
};

const totalDone = computed(() =>
  tasks.value.reduce((total, task) => (task.done ? total + 1 : total), 0)
);

function toggleDarkMode() {
  isDark.value = !isDark.value;
  const html = document.documentElement;
  if (isDark.value) {
    html.classList.add("dark");
  } else {
    html.classList.remove("dark");
  }
}

onMounted(() => {
  isDark.value = window.matchMedia("(prefers-color-scheme: dark)").matches;
  if (isDark.value) {
    document.documentElement.classList.add("dark");
  }
});
</script>

<style scoped>
.list-enter-active,
.list-leave-active {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(20px) scale(0.98);
}
.list-leave-active {
  position: absolute;
}
</style>
