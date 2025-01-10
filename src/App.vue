<script setup lang="ts">
import {ref, onMounted} from "vue";
import CommentForm from "@/components/CommentForm.vue";
import SortOptions from "@/components/SortOptions.vue";
import CommentList from "@/components/CommentList.vue";

// тип комментария
interface Comment {
  id: number;
  name: string;
  comment: string;
  date: Date;
}

// массив комментариев
const comments = ref<Comment[]>([]);

// порядок сортировки (по возрастанию или убыванию)
const sortOrder = ref<"asc" | "desc">("desc");

// загрузка комментариев из localStorage при старте
onMounted(() => {
  const storedComments = localStorage.getItem("comments");
  if (storedComments) {
    comments.value = JSON.parse(storedComments).map((comment: Comment) => ({
      ...comment,
      date: new Date(comment.date)
    }));
  }
});

// добавление нового комментария
const addComment = (playload: { name: string; comment: string }) => {
  const newComment: Comment = {
    id: Date.now(),
    name: playload.name,
    comment: playload.comment,
    date: new Date(),
  };

  comments.value.push(newComment);
  saveCommentsToLocalStorage();
};

// удаление комментария
const deleteComment = (commentId: number) => {
  comments.value = comments.value.filter(comment => comment.id !== commentId);
  saveCommentsToLocalStorage();
};

// сортировка комментариев
const sortCommentsByDate = () => {
  const isAscending = sortOrder.value === "asc";
  comments.value.sort((a, b) => {
    return isAscending
        ? a.date.getTime() - b.date.getTime()
        : b.date.getTime() - a.date.getTime();
  });

  // инвертируем порядок сортировки
  sortOrder.value = isAscending ? "desc" : "asc";
  saveCommentsToLocalStorage();
};

// функция для сохранения комментариев в localStorage
const saveCommentsToLocalStorage = () => {
  localStorage.setItem("comments", JSON.stringify(comments.value));
};
</script>

<template>
  <main>
    <CommentForm @add-comment="addComment"/>
    <SortOptions @sort="sortCommentsByDate"/>
    <CommentList :comments="comments" @delete-comment="deleteComment"/>
  </main>
</template>