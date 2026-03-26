<template>
  <ul>
    <PostItem
      v-for="post in posts"
      :key="post.no"
      :post="post"
      @delete-post="emit('delete-post', $event)"
    ></PostItem>
  </ul>
</template>

<script setup>
import PostItem from './PostItem.vue';

const props = defineProps({
  posts: Array,
});

const emit = defineEmits(['delete-post']);
</script>

<style></style>
