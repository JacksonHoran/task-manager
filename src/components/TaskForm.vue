<script setup>
import { ref } from "vue";

const taskName = ref("");
const taskDueDate = ref("");
const taskPriority = ref("");
const emit = defineEmits(["task-added"]);

const handleSubmit = () => {
  if (!taskName.value.trim()) {
    alert("Error: Invalid input provided!");
    return;
  }
  emit("task-added", {
    name: taskName.value,
    dueDate: taskDueDate.value,
    priority: taskPriority.value,
  });
  taskName.value = "";
  taskDueDate.value = "";
  taskPriority.value = "";
};
</script>

<template>
  <form
    @submit.prevent="handleSubmit"
    class="relative bg-mist-900 p-4 mx-auto flex rounded-xl items-center justify-center gap-4 text-center">
    <input
      v-model="taskName"
      type="text"
      class="w-150 flex-none h-12 px-4 text-[16px] text-white placeholder:text-white font-semibold placeholder:font-semibold bg-mist-700 rounded"
      placeholder="Title" />
    <input
      v-model="taskDueDate"
      type="date"
      class="w-39 flex-initial h-12 px-4 text-[16px] text-white placeholder:text-white font-semibold placeholder:font-semibold bg-mist-700 rounded" />
    <input
      v-model="taskPriority"
      type="text"
      class="w-34 flex-initial h-12 px-4 text-[16px] text-white placeholder:text-white font-semibold placeholder:font-semibold bg-mist-700 rounded"
      placeholder="Priority (1-10)" />
    <button
      type="submit"
      class="h-12 px-4 text-[16px] bg-mist-700 text-white font-bold hover:bg-mist-500 rounded">
      Add
    </button>
  </form>
</template>
