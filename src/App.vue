<script lang="ts" setup>
import { ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
import type { Task } from "./types";
import TaskList from "./components/TaskList.vue";

const message = ref("Welcome to the Tasks App!");
const tasks = ref<Task[]>([]);
const addTask = (newTask: string) => {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    completed: false,
  });
};

const toggleTask = (taskId: string) => {
  const task = tasks.value.find((task) => task.id === taskId);

  if (task) {
    task.completed = !task.completed;
  }
};
</script>

<template>
  <main>
    <h1 class="text-4xl font-bold my-6 text-center">{{ message }}</h1>
    <TaskForm @add-task="addTask" />
    <TaskList :tasks @toggle-task="toggleTask" />
  </main>
</template>
