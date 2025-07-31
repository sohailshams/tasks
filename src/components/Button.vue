<script lang="ts" setup>
import type { TaskFilter } from "@/types";
import { computed } from "vue";

const props = defineProps<{
  filter: TaskFilter;
  activeFilter: TaskFilter;
}>();
const emits = defineEmits<{
  setFilter: [filter: TaskFilter];
}>();
const isActive = computed(() => props.filter === props.activeFilter);
</script>

<template>
  <button
    @click="emits('setFilter', props.filter)"
    class="mx-1 bg-blue-500 w-28 h-9 text-white rounded focus:outline-none capitalize"
    :class="{
      'focus:shadow-outline bg-blue-700': isActive,
    }"
  >
    {{ props.filter }}
  </button>
</template>
