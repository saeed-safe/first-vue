<script setup>
import { onMounted, ref } from "vue";

import { usePostStore } from "@/stores/posts";
import { useRoute } from "vue-router";
import { RouterLink } from "vue-router";
import { useAuthStore } from "@/stores/auth";
const { getPost, deletePost } = usePostStore();
const route = useRoute();
const post = ref(null);
const authStore = useAuthStore();
onMounted(async () => (post.value = await getPost(route.params.id)));
</script>

<template>
  <main>
    <div v-if="post">
      <div class="border-l-4 border-blue-500 pl-4 mt-12">
        <h2 class="font-bold text-3xl">
          {{ post.title }}
        </h2>
        <p class="text-xs text-slate-600 mb-4">
          Posted By {{ post.user.name }}
        </p>
        <p>
          {{ post.body }}
          <
        </p>
        <div v-if="authStore.user && authStore.user.id == post.user_id">
          <form @submit.prevent="deletePost(post)">
            <button
              class="text-red-500 font-bold px-2 py-1 mb-2 border border-red-300"
            >
              Delete
            </button>
          </form>
          <RouterLink
            :to="{ name: 'update', params: { id: post.id } }"
            class="text-green-500 font-bold px-2 py-1 border border-green-300"
            >Update</RouterLink
          >
        </div>
      </div>
    </div>
    <div v-else>
      <h2 class="title">Page Not Found</h2>
    </div>
  </main>
</template>
