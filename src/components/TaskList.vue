<script lang="ts" setup>
import type { Task } from "@/types";
import { Card, CardHeader, CardTitle } from "./ui/card";

const props = defineProps<{
  tasks: Task[];
}>();
const emit = defineEmits<{
  toggleTask: [taskId: string];
}>();
</script>

<template>
  <p v-if="!props.tasks.length" class="text-center text-xl font-bold my-4">
    No tasks available. Please add some tasks.
  </p>
  <p v-else class="text-center text-xl font-semibold my-4">
    0 / {{ props.tasks.length }} tasks completed
  </p>
  <div class="flex flex-wrap mx-auto max-w-[90%]">
    <Card v-for="task in props.tasks" :key="task.id" class="my-4 w-32 mx-2">
      <CardHeader>
        <div class="flex items-center justify-between">
          <label for="task-status">
            <input
              @input="emit('toggleTask', task.id)"
              type="checkbox"
              :checked="task.completed"
              class="mr-2"
            />
          </label>
          <CardTitle>{{ task.title }}</CardTitle>
        </div>
      </CardHeader>
    </Card>
  </div>
</template>
