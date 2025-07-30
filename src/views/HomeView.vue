<!-- src/views/HomeView.vue -->
<script setup>
import { onMounted, ref } from "vue";
import { usePostStore } from "@/stores/posts";
import { RouterLink, RouterView } from "vue-router";
const { getAllPosts } = usePostStore();
const posts = ref([]);
onMounted(async () => (posts.value = await getAllPosts()));
</script>
<template>
  <main>
    <h1 class="title">Home Page</h1>
    <div v-if="posts.length > 0">
      <div
        v-for="post in posts"
        :key="post.id"
        class="border-l-4 border-blue-500 pl-4 mb-12"
      >
        <h2 class="font-bold text-3xl">
          {{ post.title }}
        </h2>
        <p class="text-xs text-slate-600 mb-4">
          Posted By {{ post.user.name }}
        </p>
        <p>
          {{ post.body }}
          <RouterLink
            class="text-blue-500 font-bold underline"
            :to="{
              name: 'show',
              params: { id: post.id },
            }"
          >
            Read More ..
          </RouterLink>
        </p>
      </div>
    </div>
    <div v-else>
      <h2 class="title">There Are No Posts</h2>
    </div>
  </main>
</template>
