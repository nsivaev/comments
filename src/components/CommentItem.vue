<script setup lang="ts">
import {defineProps} from "vue";

// получение комментария через props
const props = defineProps<{
  comment: {
    id: number;
    name: string;
    comment: string;
    date: Date;
    likes: number;
  }
}>();
</script>

<template>
  <div class="comment-item">
    <p>{{ props.comment.name }} ({{ props.comment.date.toLocaleString() }})</p>
    <p>{{ props.comment.comment }}</p>
    <p>{{ props.comment.likes }} 👍</p>
  </div>
</template>

<style scoped>
.comment-item {
  border: 1px solid #cccccc;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
}
</style>