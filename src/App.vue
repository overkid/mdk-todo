<template>
  <div class="app">
    <h1>Список дел</h1>

    <div class="new-task">
      <input v-model="newTitle" placeholder="Название дела" />
      <input v-model="newText" placeholder="Описание дела" />
      <button @click="addTask">Добавить</button>
    </div>

    <p>Всего дел: {{ tasks.length }}</p>

    <div class="tasks">
      <TaskItem
    v-for="task in tasks"
    :key="task.id"
    :task="task"
    @delete-task="deleteTask"
  />
    </div>

    <p v-if="tasks.length === 0">Дел пока нет</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import TaskItem from "./components/TaskItem.vue";

const tasks = ref([
  { id: 1, title: "Купить продукты", text: "Молоко и хлеб" },
  { id: 2, title: "Сделать сальто", text: "Может быть опасно" },
  { id: 3, title: "Сделать домашку", text: "Посмотреть занятие 9" }
]);

const newTitle = ref("");
const newText = ref("");

function addTask() {
  if (!newTitle.value.trim()) return;
  const newId = tasks.value.length ? Math.max(...tasks.value.map(t => Number(t.id))) + 1 : 1;
  tasks.value.push({ id: newId, title: newTitle.value, text: newText.value });
  newTitle.value = "";
  newText.value = "";
}

function deleteTask(id: number | string) {
  tasks.value = tasks.value.filter(t => t.id !== id)
}
</script>

<style>
.app {
  max-width: 720px;
  margin: 24px auto;
  font-family: Arial, sans-serif;
  padding: 0 12px;
}
.new-task {
  display: flex;
  gap: 8px;
  margin-bottom: 12px;
}
.new-task input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 6px;
}
.new-task button {
  padding: 8px 12px;
  border-radius: 6px;
  border: none;
  cursor: pointer;
}
.tasks {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>
