<script setup lang="ts">
import {ref} from "vue";
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

// массив комментариев
const comments = ref<Comment[]>([]);

// порядок сортировки (по возрастанию или убыванию)
const sortOrder = ref<"asc" | "desc">("desc");


// добавление нового комментария
const addComment = (playload: { name: string; comment: string }) => {
  const newComment: Comment = {
    id: Date.now(),
    name: playload.name,
    comment: playload.comment,
    date: new Date(),
    likes: 0
  };

  comments.value.push(newComment);
};

// сортировка комментариев
const sortComments = (sortBy: "date" | "likes") => {
  const isAscending = sortOrder.value === "asc";
  if (sortBy === "date") {
    comments.value.sort((a, b) => {
      return isAscending
          ? a.date.getTime() - b.date.getTime()
          : b.date.getTime() - a.date.getTime();
    });
  } else if (sortBy === "likes") {
    comments.value.sort((a, b) => {
      return isAscending ? a.likes - b.likes : b.likes - a.likes;
    });
  }

  // инвертируем порядок сортировки
  sortOrder.value = isAscending ? "desc" : "asc";
};

</script>

<template>
  <main>
    <CommentForm @add-comment="addComment"/>
    <SortOptions @sort="sortComments"/>
    <CommentList :comments="comments"/>
  </main>
</template>

<style scoped>

</style>
