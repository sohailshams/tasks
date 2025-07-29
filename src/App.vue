<script lang="ts" setup>
import { ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
import type { Task } from "./types";

const message = ref("Welcome to the Tasks App!");
const tasks = ref<Task[]>([]);
const addTask = (newTask: string) => {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    completed: false,
  });
  console.log(`New task added: ${newTask}`);
};
</script>

<template>
  <div class="flex flex-col items-center justify-center py-1 bg-gray-100">
    <h1 class="text-4xl font-bold mb-6">{{ message }}</h1>
    <TaskForm @add-task="addTask" />
    <ul class="list-disc pl-5">
      <li v-for="task in tasks" :key="task.id" class="mb-2">
        {{ task.title }} -
        <span :class="{ 'line-through': task.completed }">
          {{ task.completed ? "Completed" : "Pending" }}
        </span>
      </li>
    </ul>
  </div>
</template>
