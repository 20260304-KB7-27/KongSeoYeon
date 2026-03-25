<template>
  <div>
    <input v-model="title" placeholder="제목" />
    <input v-model="content" placeholder="내용" />
    <button @click="add">작성</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['add-post']); // 부모한테 이벤트 보내겠다고 선언

const title = ref('');
const content = ref('');

const add = () => {
  if (!title.value || !content.value) return;

  emit('add-post', {
    title: title.value,
    content: content.value,
  });

  title.value = '';
  content.value = '';
};
</script>

<style lang="scss" scoped>
input {
  margin-right: 5px;
}
</style>
