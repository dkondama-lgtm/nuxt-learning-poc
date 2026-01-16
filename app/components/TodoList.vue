<template>
  <ul class="list-group">
    <li
      v-for="todo in todos"
      :key="todo.id"
      class="list-group-item d-flex align-items-center justify-content-between"
    >
      <div class="form-check">
        <input
          class="form-check-input"
          type="checkbox"
          :id="`todo-${todo.id}`"
          :checked="todo.done"
          @change="$emit('toggle', todo.id)"
        />
        <label
          class="form-check-label"
          :for="`todo-${todo.id}`"
          :class="{ 'text-decoration-line-through text-muted': todo.done }"
        >
          {{ todo.text }}
        </label>
      </div>

      <button
        type="button"
        class="btn btn-sm btn-outline-danger"
        aria-label="Remove todo"
        @click="$emit('remove', todo.id)"
      >
        ✕
      </button>
    </li>

    <li v-if="!todos.length" class="list-group-item text-muted text-center">
      No todos yet
    </li>
  </ul>
</template>

<script setup lang="ts">
interface Todo {
  id: number;
  text: string;
  done: boolean;
}

defineProps<{
  todos: Todo[];
}>();

defineEmits<{
  (e: "toggle", id: number): void;
  (e: "remove", id: number): void;
}>();
</script>
