<script lang="ts" setup>
import { ref } from "vue";

const emit = defineEmits<{
  addTask: [task: string];
}>();
const newTask = ref("");
const err = ref("");
const taskSubmitHandler = () => {
  if (newTask.value.trim()) {
    emit("addTask", newTask.value.trim());
    newTask.value = "";
  } else {
    err.value = "Task cannot be empty!";
  }
};
</script>

<template>
  <form @submit.prevent="taskSubmitHandler">
    <div class="mb-4">
      <label for="task" class="block text-gray-700 text-sm font-bold mb-2">
        New Task:
        <input
          v-model="newTask"
          @input="err = ''"
          name="task"
          type="text"
          id="task"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          placeholder="Enter your task here"
        />
      </label>
      <p v-if="err" class="text-red-500">{{ err }}</p>
    </div>
    <button
      type="submit"
      class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
    >
      Add Task
    </button>
  </form>
</template>
