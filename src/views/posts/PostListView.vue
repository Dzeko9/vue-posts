<template>
  <div>
    <h2 class="mt-4">게시글 목록</h2>
    <hr class="my-4" />
    <div class="row g-3">
      <div v-for="post in posts" :key="post.id" class="col-4">
        <PostItem :title="post.title" :content="post.content" :created-at="post.createdAt" @click="goPage(post.id)" />
      </div>
    </div>
    <hr class="my-4" />
    <AppCard>
      <PostDetailView :id="1"></PostDetailView>
    </AppCard>
  </div>
</template>

<script setup>
import PostItem from "@/components/posts/PostItem.vue";
import PostDetailView from "@/views/posts/PostDetailView.vue";
import AppCard from "@/components/AppCard.vue";

import { getPosts } from "@/api/posts";
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const posts = ref([]);

const fetchPosts = async () => {
  try {
    const { data } = await getPosts();
    posts.value = data;
  } catch (error) {
    console.error(error);
  }
};

fetchPosts();

const goPage = (id) => {
  // router.push(`/posts/${id}`);
  // http://localhost:5173/posts/2?searchText=hello#world!
  router.push({
    name: "PostDetail",
    params: {
      id,
    },
  });
};
</script>

<style lang="scss" scoped></style>
