<template>
  <div class="todo-input d-flex gap-2">
    <label for="todo-input" class="visually-hidden"> Add todo </label>

    <input
      id="todo-input"
      class="form-control"
      type="text"
      :placeholder="placeholder"
      :value="modelValue"
      @input="onInput"
      @keydown.enter.prevent="onAdd"
      aria-label="Todo text"
    />

    <button
      type="button"
      class="btn btn-primary"
      @click="onAdd"
      :disabled="!trimmed"
      aria-label="Add todo"
    >
      Add
    </button>
  </div>
</template>

<script setup lang="ts">
import { computed } from "vue";

interface Props {
  modelValue?: string;
  placeholder?: string;
}

const props = defineProps<Props>();

const emit = defineEmits<{
  (e: "update:modelValue", value: string): void;
  (e: "add"): void;
}>();

const trimmed = computed(() => (props.modelValue ?? "").trim());

function onInput(e: Event) {
  emit("update:modelValue", (e.target as HTMLInputElement).value);
}

function onAdd() {
  if (!trimmed.value) return;
  emit("add");
}
</script>

<style scoped>
.todo-input {
  align-items: flex-start;
}

.form-control {
  min-width: 0;
  flex: 1 1 auto;
}

.btn[disabled] {
  opacity: 0.6;
  pointer-events: none;
}

.visually-hidden {
  position: absolute !important;
  height: 1px;
  width: 1px;
  overflow: hidden;
  clip: rect(1px, 1px, 1px, 1px);
  white-space: nowrap;
  border: 0;
  padding: 0;
  margin: -1px;
}
</style>
