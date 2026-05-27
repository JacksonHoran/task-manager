<script setup>
import { ref } from "vue";
const props = defineProps({ task: Object });

const emit = defineEmits(["task-remove"]);

const remove = () => {
  emit("task-remove", props.task.id);
};
</script>

<template>
  <div
    class="flex items-center justify-between px-4 py-3 rounded cursor-pointer transition-all bg-mist-700 text-white hover:bg-mist-500">
    <p class="truncate max-w-full font-semibold">{{ task.name }}</p>
    <button
      @click.stop="remove"
      class="px-3 py-1 rounded bg-mist-900 text-white hover:bg-mist-700">
      Remove
    </button>
  </div>
</template>
