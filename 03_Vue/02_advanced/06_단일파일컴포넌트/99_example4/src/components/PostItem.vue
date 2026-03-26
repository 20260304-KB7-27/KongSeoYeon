<template>
  <li class="post-item">
    <!-- 제목 -->
    <div
      @click="isOpen = !isOpen"
      style="display: flex; justify-content: space-between"
    >
      {{ post.no }}. {{ post.title }}
      <span class="arrow">{{ isOpen ? '▲' : '▼' }}</span>
    </div>

    <!-- 내용 -->
    <div v-if="isOpen" class="post-content">
      <!-- 수정 모드 -->
      <div v-if="post.isEditing" class="edit-box">
        <input v-model="post.editTitle" />
        <textarea v-model="post.editContent"></textarea>
        <button @click="save">저장</button>
        <button @click="cancel">취소</button>
      </div>

      <!-- 일반 모드 -->
      <div v-else>
        <h3>{{ post.title }}</h3>
        <p>{{ post.content }}</p>

        <button @click="edit">수정</button>
        <button @click="remove">삭제</button>
        <button @click="close">닫기</button>
      </div>
    </div>
  </li>
</template>

<script setup>
import { ref } from 'vue';

const isOpen = ref(false);
const props = defineProps({
  post: Object,
});

const emit = defineEmits(['delete-post']);

// 수정
const edit = () => {
  props.post.editTitle = props.post.title;
  props.post.editContent = props.post.content;
  props.post.isEditing = true;
};

// 저장
const save = () => {
  props.post.title = props.post.editTitle;
  props.post.content = props.post.editContent;
  props.post.isEditing = false;
};

// 취소
const cancel = () => {
  props.post.isEditing = false;
};

// 삭제
const remove = () => {
  if (confirm('정말로 삭제하시겠습니까?')) {
    emit('delete-post', props.post);
  }
};

const close = () => {
  isOpen.value = false;
};
</script>

<style></style>
