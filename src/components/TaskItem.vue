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
    class="flex items-center justify-between px-4 py-3 rounded cursor-pointer transition-all bg-white text-black hover:bg-slate-50">
    <p class="truncate">{{ task.name }}</p>
    <button
      @click.stop="remove"
      class="px-3 py-1 rounded bg-blue-400 text-blue-950">
      Remove
    </button>
  </div>
</template>

<style scoped>
.truncate {
  max-width: 100%;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>
