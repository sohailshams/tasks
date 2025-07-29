<script lang="ts" setup>
import { ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
import type { Task } from "./types";
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from "./components/ui/card";

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
  <div>
    <h1 class="text-4xl font-bold my-6 text-center">{{ message }}</h1>
    <TaskForm @add-task="addTask" />
    <div class="flex flex-wrap mx-auto max-w-[90%]">
      <Card v-for="task in tasks" :key="task.id" class="my-4 w-32 mx-2">
        <CardHeader>
          <CardTitle>{{ task.title }}</CardTitle>
          {{ task.completed ? "Completed" : "Pending" }}
        </CardHeader>
      </Card>
    </div>
  </div>
</template>
