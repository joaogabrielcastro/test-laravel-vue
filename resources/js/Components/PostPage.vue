<template>
  <PostForm @post-created="fetchPosts" />
  <PostList :posts="posts" />
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

import PostForm from './PostForm.vue';
import PostList from './PostList.vue';

const posts = ref([]);

const fetchPosts = async () => {
  try {
    const response = await axios.get('/api/posts');
    posts.value = response.data;
  } catch (error) {
    console.error('Erro ao buscar posts:', error);
  }
};

onMounted(() => {
  fetchPosts();
});
</script>
