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
      likes: number;
    }[];
  }>();
</script>

<template>
  <p>comment list</p>
  <CommentItem/>
</template>
