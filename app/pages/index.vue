<template>
  <main class="container py-4">
    <h1 class="mb-4">Articles</h1>

    <!-- Loading state -->
    <div v-if="pending" class="row g-3">
      <div v-for="n in 3" :key="n" class="col-12 col-md-6 col-lg-4">
        <article class="card h-100">
          <div
            class="card-img-top placeholder-glow"
            style="height: 160px; background: #f0f0f0"
          ></div>

          <div class="card-body">
            <h2 class="h6 mb-2 placeholder-glow">
              <span class="placeholder col-6"></span>
            </h2>

            <p class="text-muted mb-3 placeholder-glow">
              <span class="placeholder col-12"></span>
            </p>

            <div class="d-flex justify-content-between align-items-center">
              <small class="text-muted placeholder col-4"></small>
              <span
                class="btn btn-sm btn-primary disabled placeholder col-2"
              ></span>
            </div>
          </div>
        </article>
      </div>
    </div>

    <!-- Error state -->
    <div v-else-if="error" class="alert alert-danger">
      <strong>Failed to load articles.</strong>
      <div style="white-space: pre-wrap; word-break: break-word">
        {{ errorMessage }}
      </div>
    </div>

    <!-- Content state -->
    <div v-else class="row g-3">
      <div
        v-for="article in articles"
        :key="article.id"
        class="col-12 col-md-6 col-lg-4"
      >
        <ArticleCard
          :id="article.id"
          :title="article.title"
          :excerpt="article.excerpt"
          :author="article.author"
          :date="article.date"
          :image="article.image"
          @read="onRead"
        />
      </div>
    </div>

    <!-- Selected / feedback -->
    <div v-if="selected" class="mt-4 alert alert-info">
      You clicked:
      <strong>{{ selected.title }}</strong>
    </div>
  </main>
</template>

<script setup>
import { computed, ref } from "vue";
import ArticleCard from "~/components/ArticleCard.vue";

const { data, pending, error } = await useFetch("/articles.json", {
  server: false,
});

const errorMessage = computed(() => {
  const e = error.value;
  return e?.message || e?.statusMessage || String(e);
});

const articles = computed(() => {
  const d = data?.value;
  if (!d) return [];
  if (Array.isArray(d.articles)) return d.articles;
  if (Array.isArray(d)) return d;
  return [];
});

const selected = ref(null);

function onRead(articleId) {
  const found = (articles.value || []).find((a) => a.id === articleId);
  selected.value = found ?? null;
  console.log("Read clicked for id:", articleId);
}
</script>
