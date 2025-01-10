<script setup lang="ts">
import {defineProps, defineEmits} from "vue";

// получение комментария через props
const props = defineProps<{
  comment: {
    id: number;
    name: string;
    comment: string;
    date: Date;
  }
}>();

// эмит для удаления комментария
const emit = defineEmits<{
  (e: "delete", commentId: number): void;
}>();

// удаление комментария
const deleteComment = () => {
  emit("delete", props.comment.id);
};
</script>

<template>
  <div class="comment-item">
    <p>{{ props.comment.name }} ({{ props.comment.date.toLocaleString() }})</p>
    <p>{{ props.comment.comment }}</p>
    <button @click="deleteComment">🗑️ Удалить</button>
  </div>
</template>

<style scoped>
.comment-item {
  border: 1px solid #cccccc;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;

  button {
    margin-top: 10px;
    padding: 5px 10px;
    border: 1px solid #cccccc;
    border-radius: 5px;
    cursor: pointer;
  }
}
</style>