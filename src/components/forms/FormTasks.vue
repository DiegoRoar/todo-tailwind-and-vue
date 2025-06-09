<template>
  <form @submit.prevent="formSubmitted">
    <BaseInput
      label="New Task"
      v-model="newTask"
      :class="{ 'border-red-500': errorMessage }"
      @input="errorMessage = ''"
    />
    <p v-if="errorMessage" class="text-red-500 text-sm mt-1">
      {{ errorMessage }}
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

const formSubmitted = () => {
  if (newTask.value.trim()) {
    emit("addTask", newTask.value.trim());
    newTask.value = "";
    errorMessage.value = "";
  } else {
    errorMessage.value = "Task cannot be empty";
  }
};
</script>

<style scoped>
.button-container {
  display: flex;
  justify-content: flex-end;
}
</style>
