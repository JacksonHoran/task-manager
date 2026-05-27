<script setup>
import { ref } from "vue";

const taskName = ref("");
const emit = defineEmits(["task-added"]);

const handleSubmit = () => {
  if (!taskName.value.trim()) {
    alert("Error: Invalid input provided!");
    return 
  };
  emit("task-added", taskName.value);
  taskName.value = "";
};
</script>

<template>
  <form
    @submit.prevent="handleSubmit"
    class="relative bg-mist-900 p-4 mx-auto flex rounded-xl items-center justify-center gap-4 text-center"
  >
    <input
      v-model="taskName"
      type="text"
      class="flex-1 h-12 px-4 text-[16px] text-white font-semibold placeholder:font-semibold placeholder:text-mist-300 outline-none bg-mist-700 rounded"
      placeholder="Add a new task..."
    />
    <button
      type="submit"
      class="h-12 px-4 text-[16px] bg-mist-700 text-white font-bold hover:bg-mist-500 rounded"    >
      Add task
    </button>
  </form>
</template>
