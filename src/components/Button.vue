<script lang="ts" setup>
import type { TaskFilter } from "@/types";

const props = defineProps<{
  filter: TaskFilter;
}>();
const emits = defineEmits<{
  setFilter: [filter: TaskFilter];
}>();
</script>

<template>
  <button
    @click="emits('setFilter', props.filter)"
    class="mx-1 bg-blue-500 hover:bg-blue-700 w-28 h-9 text-white rounded focus:outline-none focus:shadow-outline capitalize"
  >
    {{ props.filter }}
  </button>
</template>
