<template>
  <main class="container py-4">
    <h1 class="mb-3">Todo</h1>

    <!-- input component -->
    <div class="mb-3">
      <TodoInput
        v-model="draft"
        placeholder="Add a new todo and press Enter or Add"
        @add="handleAdd"
      />
    </div>

    <!-- list component -->
    <TodoList :todos="todos" @toggle="handleToggle" @remove="handleRemove" />

    <!-- simple summary -->
    <div class="mt-3">
      <small class="text-muted">
        {{ todos.length }} item(s) • {{ completedCount }} completed
      </small>
    </div>

    <!-- back link -->
    <div class="mt-4">
      <NuxtLink to="/" class="btn btn-sm btn-outline-secondary"
        >Back to home</NuxtLink
      >
    </div>
  </main>
</template>

<script setup lang="ts">
import { computed, ref } from "vue";
import TodoInput from "~/components/TodoInput.vue";
import TodoList from "~/components/TodoList.vue";

interface Todo {
  id: number;
  text: string;
  done: boolean;
}

const todos = ref<Todo[]>([]);
const draft = ref("");
const nextId = ref(1);
const completedCount = computed(() => todos.value.filter((t) => t.done).length);
function handleAdd() {
  const text = draft.value.trim();
  if (!text) return;

  todos.value = [
    ...todos.value,
    { id: nextId.value++, text, done: false } as Todo,
  ];

  draft.value = "";
}

function handleToggle(id: number) {
  todos.value = todos.value.map((t) =>
    t.id === id ? { ...t, done: !t.done } : t
  );
}

function handleRemove(id: number) {
  todos.value = todos.value.filter((t) => t.id !== id);
}
</script>

<style scoped>
.container {
  max-width: 780px;
}
</style>
