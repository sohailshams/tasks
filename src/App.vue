<script lang="ts" setup>
import { computed, ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
import { type TaskFilter, type Task } from "./types";
import TaskList from "./components/TaskList.vue";
import Button from "./components/Button.vue";

const message = ref("Welcome to the Tasks App!");
const tasks = ref<Task[]>([]);
const filter = ref<TaskFilter>("all");

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

const removeTask = (taskId: string) => {
  tasks.value = tasks.value.filter((task) => task.id !== taskId);
};

const totalCompleted = computed(() => {
  return tasks.value.filter((task) => task.completed).length;
});

const filteredTasks = computed(() => {
  if (filter.value === "all") {
    return tasks.value;
  } else if (filter.value === "todo") {
    return tasks.value.filter((task) => !task.completed);
  } else if (filter.value === "done") {
    return tasks.value.filter((task) => task.completed);
  }
  return tasks.value;
});

const setFilter = (filterValue: TaskFilter) => {
  filter.value = filterValue;
};
</script>

<template>
  <main>
    <h1 class="text-4xl font-bold my-6 text-center">{{ message }}</h1>
    <TaskForm @add-task="addTask" />
    <div class="flex items-center justify-center space-x-4 mt-2">
      <p v-if="!tasks.length" class="text-center text-xl font-bold my-4">
        No tasks available. Please add some tasks.
      </p>
      <p v-else class="text-center text-xl font-semibold my-4">
        {{ totalCompleted }} / {{ tasks.length }} tasks completed
      </p>
      <div v-if="tasks.length">
        <Button :activeFilter="filter" filter="all" @set-filter="setFilter" />
        <Button :activeFilter="filter" filter="todo" @set-filter="setFilter" />
        <Button :activeFilter="filter" filter="done" @set-filter="setFilter" />
      </div>
    </div>
    <TaskList
      :tasks="filteredTasks"
      @toggle-task="toggleTask"
      @remove-task="removeTask"
    />
  </main>
</template>
