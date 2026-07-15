<template>
  <section class="detail-page">
    <div class="detail-card">
      <span class="post-chip">{{ post.category }}</span>
      <h1>{{ post.title }}</h1>
      <p class="meta">{{ post.time }} · 조회 {{ post.views }}</p>
      <div class="content">{{ post.content }}</div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import { posts as mockPosts } from '../data/homeMock'

const route = useRoute()
const post = computed(() => mockPosts.find((item) => item.id === Number(route.params.id)) || mockPosts[0])
</script>

<style scoped>
.detail-page {
  display: flex;
  justify-content: center;
}

.detail-card {
  width: 100%;
  max-width: 860px;
  padding: 28px;
  border: 1px solid var(--line);
  border-radius: 24px;
  background: rgba(255,255,255,0.92);
  box-shadow: var(--shadow);
}

.post-chip {
  display: inline-block;
  padding: 6px 10px;
  border-radius: 999px;
  background: var(--green-100);
  color: var(--green-900);
  font-size: 11px;
  font-weight: 800;
}

.detail-card h1 {
  margin: 14px 0 8px;
  color: var(--navy);
  font-size: clamp(24px, 2.4vw, 32px);
}

.meta {
  color: #6b736f;
  font-size: 13px;
}

.content {
  margin-top: 18px;
  color: #4d554f;
  line-height: 1.8;
  white-space: pre-line;
}
</style>