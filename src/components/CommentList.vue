<script setup lang="ts">
import {defineProps} from "vue";
import CommentItem from "@/components/CommentItem.vue";

// получение списка комментариев через props
const props = defineProps<{
  comments: {
    id: number;
    name: string;
    comment: string;
    date: Date;
    likes: number;
  }[];
}>();
</script>

<template>
  <div class="app__comments">
    <p class="app__comments-text" v-if="props.comments.length === 0">Комментариев нет</p>
    <div class="app__comment" v-for="comment in props.comments" :key="comment.id">
      <CommentItem :comment="comment"/>
    </div>
  </div>
</template>
