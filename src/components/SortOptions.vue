<script setup lang="ts">
import { defineEmits } from 'vue';

// событие для выбора сортировки
const emit = defineEmits<{
  (e: "sort", playload: "date"): void;
}>();

// функция выбора сортировки
const onSortChange = (sortBy: "date") => {
  emit("sort", sortBy);
};
</script>

<template>
  <div class="sort-options">
    <button @click="onSortChange('date')">Сортировать по дате</button>
  </div>
</template>


<style scoped>
.sort-options {
  margin-bottom: 10px;
  display: flex;
  gap: 10px;

  button {
    padding: 5px 10px;
    border: 1px solid #cccccc;
    border-radius: 5px;
    cursor: pointer;
  }
}
</style>