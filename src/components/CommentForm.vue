<script setup lang="ts">
import {ref} from "vue";

// поля формы
const name = ref("");
const comment = ref("");

// передача данных наверх
const emit = defineEmits<{
  (e: "add-comment", playload: { name: string; comment: string }): void
}>();

// отправка формы
const submitForm = () => {
  if (name.value.trim() && comment.value.trim()) {
    emit("add-comment", {
      name: name.value,
      comment: comment.value,
    });

    // очистка полей
    name.value = "";
    comment.value = "";
  } else {
    alert("Введите имя и комментарий");
  }
};
</script>

<template>
  <form class="comment-form" @submit.prevent="submitForm">
    <input
        type="text"
        v-model="name"
        placeholder="Имя"
        required
    />
    <textarea
        v-model="comment"
        placeholder="Комментарий"
        required
    ></textarea>
    <button type="submit">Отправить</button>
  </form>
</template>

<style scoped>
.comment-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
  max-width: 400px;
  margin-inline: auto;
}
</style>
