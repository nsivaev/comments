<script setup lang="ts">
  import { ref } from "vue";
  import CommentForm from "@/components/CommentForm.vue";
  import SortOptions from "@/components/SortOptions.vue";
  import CommentList from "@/components/CommentList.vue";

  // тип комментария
  interface Comment {
    id: number;
    name: string;
    comment: string;
    date: Date;
    likes: number;
  }

  // массив комментарие
  const comments = ref<Comment[]>([]);

  // добавление нового комментария
  const addComment = (playload: { name: string; comment: string }) => {
    const newComment: Comment = {
      id: Date.now(),
      name: playload.name,
      comment: playload.comment,
      date: new Date(),
      likes: 0
    }

    comments.value.push(newComment);
  }
</script>

<template>
  <main>
    <CommentForm @add-comment="addComment" />
    <SortOptions/>
    <CommentList :comments="comments" />
  </main>
</template>

<style scoped>

</style>
