<script setup lang="ts">
import { defineProps } from "vue";
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
</script>

<template>
  <h3 class="comment-list__title">Комментарии</h3>
  <div class="comment-list">
    <p class="comment-list__text" v-if="props.comments.length === 0">Комментариев нет</p>
    <div class="comment-list__item" v-for="comment in props.comments" :key="comment.id">
      <CommentItem :comment="comment"/>
    </div>
  </div>
</template>
