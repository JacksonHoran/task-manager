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
    class="relative bg-slate-800 p-4 mx-auto flex rounded-xl items-center justify-center gap-4 text-center"
  >
    <input
      v-model="taskName"
      type="text"
      class="relative z-10 pointer-events-auto w-full max-w-2xl p-2.5 text-[16px] text-blue-100 font-bold outline-none bg-blue-500 rounded placeholder:text-blue-950/60"
      placeholder="Add a new task..."
    />
    <button
      type="submit"
      class="relative z-10 pointer-events-auto w-30 max-w-2xl p-2.5 text-[20px] bg-blue-400 text-blue-100 font-bold transition-all duration-300 hover:bg-blue-200 cursor-pointer rounded"
    >
      Add task
    </button>
  </form>
</template>
