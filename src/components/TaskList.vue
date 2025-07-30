<script lang="ts" setup>
import type { Task } from "@/types";
import { Card, CardHeader, CardTitle } from "./ui/card";
import { computed } from "vue";

const props = defineProps<{
  tasks: Task[];
}>();

const emits = defineEmits<{
  toggleTask: [taskId: string];
  removeTask: [taskId: string];
}>();

const totalCompleted = computed(() => {
  return props.tasks.filter((task) => task.completed).length;
});
</script>

<template>
  <p v-if="!props.tasks.length" class="text-center text-xl font-bold my-4">
    No tasks available. Please add some tasks.
  </p>
  <p v-else class="text-center text-xl font-semibold my-4">
    {{ totalCompleted }} / {{ props.tasks.length }} tasks completed
  </p>
  <div class="flex flex-wrap mx-auto max-w-[90%]">
    <Card v-for="task in props.tasks" :key="task.id" class="my-4 w-48 mx-2">
      <div class="flex items-center justify-between">
        <CardHeader>
          <div class="flex items-center">
            <label for="task-status">
              <input
                @input="emits('toggleTask', task.id)"
                type="checkbox"
                :checked="task.completed"
                class="mr-2"
              />
            </label>
            <CardTitle :class="{ 'line-through': task.completed }">
              {{ task.title }}
            </CardTitle>
          </div>
        </CardHeader>
        <svg
          @click="emits('removeTask', task.id)"
          class="h-4 mr-4 cursor-pointer"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 448 512"
        >
          <path
            d="M136.7 5.9L128 32 32 32C14.3 32 0 46.3 0 64S14.3 96 32 96l384 0c17.7 0 32-14.3 32-32s-14.3-32-32-32l-96 0-8.7-26.1C306.9-7.2 294.7-16 280.9-16L167.1-16c-13.8 0-26 8.8-30.4 21.9zM416 144L32 144 53.1 467.1C54.7 492.4 75.7 512 101 512L347 512c25.3 0 46.3-19.6 47.9-44.9L416 144z"
          />
        </svg>
      </div>
    </Card>
  </div>
</template>
