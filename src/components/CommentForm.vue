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
    alert("✏️ Введите имя и комментарий");
  }
};
</script>

<template>
  <h1 class="comment-form__title">✏️ Введите имя и комментарий</h1>
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
        rows="5"
    ></textarea>
    <button type="submit">Отправить</button>
  </form>
</template>

<style scoped>
.comment-form__title {
  margin-bottom: 20px;
}

.comment-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
  max-width: 400px;
  margin-right: auto;

  input {
    height: 40px;
    padding: 0 10px;
    border: 1px solid #cccccc;
    border-radius: 20px;
  }

  textarea {
    padding: 10px;
    border: 1px solid #cccccc;
    border-radius: 20px;
    resize: none;
  }

  textarea::-webkit-resizer {
    display: none;
  }

  button {
    height: 40px;
    border: 1px solid #cccccc;
    border-radius: 20px;
    cursor: pointer;
  }
}
</style>
