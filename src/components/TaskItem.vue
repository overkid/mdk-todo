<template>
  <div class="task-card">
    <h3>{{ task.title }}</h3>
    <p>{{ task.text }}</p>
    <button class="delete-btn" @click="$emit('delete-task', task.id)">Удалить</button>
  </div>
</template>

<script setup lang="ts">
const props = defineProps<{
  task: { id: number | string; title: string; text: string }
}>()
</script>

<style scoped>
.task-card {
  border: 1px solid #ddd;
  padding: 12px;
  border-radius: 8px;
  background: #fff;
  position: relative;
  text-align: left; /* добавлено выравнивание текста по левому краю */
}

.task-card h3 {
  margin: 0 0 2px 0;
  font-size: 18px;
  color: black;
}

.task-card p {
  margin: 0;
  color: #444;
}
.delete-btn {
  position: absolute;
  top: 8px;
  right: 8px;
  border: none;
  background: #ff5555;
  color: white;
  padding: 4px 8px;
  border-radius: 4px;
  cursor: pointer;
}
</style>
