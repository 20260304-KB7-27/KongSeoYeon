<template>
  <li class="post-item">
    <!-- 제목 -->
     <div class="header">
        {{ post.no }}. {{ post.title }}
     </div>

     <!-- 내용 -->
      <div class="content">
        <!-- 수정 모드 -->
         <div v-if="post.isEditing" class="edit-box">
            
         </div>
      </div>
  </li>
</template>

<script setup>
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
  if (confirm('정말 삭제할까요?')) {
    emit('delete-post', props.post);
  }
};
</script>

<style lang="scss" scoped></style>
