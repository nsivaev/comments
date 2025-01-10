<script setup lang="ts">
import { defineProps, defineEmits } from "vue";
import CommentItem from "@/components/CommentItem.vue";

// получение списка комментариев через props
const props = defineProps<{
  comments: {
    id: number;
    name: string;
    comment: string;
    date: Date;
  }[];
}>();

// эмит для удаления комментария
const emit = defineEmits<{
  (e: "delete-comment", commentId: number): void;
}>();

// передача id комментария на удаление
const handleDelete = (commentId: number) => {
  emit("delete-comment", commentId);
};
</script>

<template>
  <h3 class="comment-list__title">Комментарии</h3>
  <div class="comment-list">
    <p class="comment-list__text" v-if="props.comments.length === 0">Комментариев нет</p>
    <div class="comment-list__item" v-for="comment in props.comments" :key="comment.id">
      <CommentItem :comment="comment" @delete="handleDelete"/>
    </div>
  </div>
</template>
