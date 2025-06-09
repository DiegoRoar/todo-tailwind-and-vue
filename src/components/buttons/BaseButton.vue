<template>
  <button :type="props.type" :disabled="props.disabled" class="btn-primary">
    <slot></slot>
  </button>
</template>

<script lang="ts" setup>
const props = defineProps<{
  type?: "button" | "submit" | "reset";
  disabled?: boolean;
}>();
defineEmits(["update:modelValue"]);
</script>

<style scoped></style>
