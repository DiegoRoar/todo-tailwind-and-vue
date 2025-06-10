<template>
  <div class="flex flex-col gap-1 w-full">
    <label v-if="props.label" class="label-default w-full">
      {{ props.label }}
      <input
        :id="props.id"
        :type="props.type || 'text'"
        :placeholder="props.placeholder"
        :value="props.modelValue"
        class="input-default py-8"
        :aria-invalid="props.ariaInvalid === true ? 'true' : undefined"
        :class="[$attrs.class]"
        @input="onInput"
        maxlength="50"
      />
    </label>
  </div>
</template>

<script lang="ts" setup>
const props = defineProps<{
  modelValue?: string;
  label?: string;
  placeholder?: string;
  type?: string;
  id?: string;
  ariaInvalid?: boolean;
}>();
const emit = defineEmits(["update:modelValue"]);

function onInput(event: Event) {
  const target = event.target as HTMLInputElement | null;
  if (target) emit("update:modelValue", target.value);
}
</script>

<style scoped>
/* No @apply or border styles here, handled globally */
</style>
