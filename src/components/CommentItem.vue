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
</script>

<template>
  <div class="comment-item">
    <p>{{ props.comment.name }} ({{ props.comment.date.toLocaleString() }})</p>
    <p>{{ props.comment.comment }}</p>
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