<template>
  <main
    class="w-full h-screen bg-gradient-to-br from-blue-100 via-purple-100 to-pink-100"
  >
    <div
      class="w-full sm:w-[95%] mx-auto h-screen bg-gray-50 shadow-2xl shadow-gray-400/60 border border-gray-200"
    >
      <BaseButton type="button"> Click me</BaseButton>
      <BaseInput label="test" placeholder="testing the input" type="text" />
    </div>
  </main>
</template>

<script lang="ts" setup>
import BaseButton from "./components/buttons/BaseButton.vue";
import BaseInput from "./components/inputs/BaseInput.vue";
</script>

<style scoped></style>
