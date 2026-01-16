<template>
  <article
    class="card h-100 shadow-sm"
    role="article"
    :aria-labelledby="titleId"
  >
    <img
      :src="imgSrc"
      :alt="title"
      loading="lazy"
      class="card-img-top"
      @error="onImgError"
    />

    <div class="card-body d-flex flex-column">
      <h2 :id="titleId" class="h6 mb-2">
        {{ title }}
      </h2>

      <p class="text-muted mb-3">
        {{ excerpt }}
      </p>

      <div class="mt-auto d-flex justify-content-between align-items-center">
        <small class="text-muted"> {{ author }} • {{ date }} </small>

        <button
          class="btn btn-sm btn-primary"
          @click="onRead"
          :aria-label="`Read ${title}`"
        >
          Read
        </button>
      </div>
    </div>
  </article>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

interface Props {
  id: string;
  title: string;
  excerpt: string;
  author: string;
  date: string;
  image: string;
  content?: string;
}

const props = defineProps<Props>();
const titleId = computed(() => `article-title-${props.id}`);
const FALLBACK = "https://via.placeholder.com/600x400?text=No+Image";
const imgSrc = ref(props.image || FALLBACK);

function onImgError() {
  if (imgSrc.value !== FALLBACK) {
    imgSrc.value = FALLBACK;
  }
}

const emit = defineEmits<{
  (e: "read", id: string): void;
}>();

function onRead() {
  emit("read", props.id);
}
</script>

<style scoped>
.card-img-top {
  height: 160px;
  object-fit: cover;
  background: #f8f9fa;
}
</style>
