<template>
  <form
    @submit.prevent="formSubmitted"
    class="flex flex-col gap-4 w-full justify-center items-center"
  >
    <BaseInput
      label="New Task"
      v-model="newTask"
      :aria-invalid="!!errorMessage"
      :class="{ success: TaskAdded && !errorMessage }"
      @input="clearMessages"
    />
    <p v-if="errorMessage" class="text-red-500 text-sm mt-1">
      {{ errorMessage }}
    </p>
    <p v-else-if="TaskAdded" class="text-green-500 text-sm mt-1">
      {{ TaskAdded }}
    </p>
    <div class="button-container">
      <BaseButton>Add</BaseButton>
    </div>
  </form>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import BaseInput from "../inputs/BaseInput.vue";
import BaseButton from "../buttons/BaseButton.vue";

const emit = defineEmits<{
  addTask: [newTask: string];
}>();

const newTask = ref("");
const errorMessage = ref("");
const TaskAdded = ref("");

const formSubmitted = () => {
  if (newTask.value.trim()) {
    emit("addTask", newTask.value.trim());
    newTask.value = "";
    errorMessage.value = "";
    TaskAdded.value = "Task added successfully!";
  } else {
    errorMessage.value = "Task cannot be empty";
  }
};

function clearMessages() {
  errorMessage.value = "";
  TaskAdded.value = "";
}
</script>

<style scoped>
.button-container {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: flex-end;
}
</style>
