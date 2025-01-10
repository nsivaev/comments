<script setup lang="ts">
import { defineEmits } from 'vue';

// событие для выбора сортировки
const emit = defineEmits<{
  (e: "sort", playload: "date" | "likes"): void;
}>();

// функция выбора сортировки
const onSortChange = (sortBy: "date" | "likes") => {
  emit("sort", sortBy);
};
</script>

<template>
  <div class="sort-options">
    <button @click="onSortChange('date')">Сортировать по дате</button>
    <button @click="onSortChange('likes')">Сортировать по лайкам</button>
  </div>
</template>


<style scoped>
.sort-options {
  display: flex;
  gap: 10px;
}
</style>