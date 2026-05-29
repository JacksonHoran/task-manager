<script setup>
import { ref } from "vue";
import TaskSort from "./TaskSort.vue";

const taskName = ref("");
const taskDueDate = ref("");
const taskPriority = ref("Low");
const sortBy = defineModel("sortBy");
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
  taskPriority.value = "Low";
};
</script>

<template>
  <div class="flex gap-50">
    <div class="flex-1">
      <TaskSort v-model="sortBy" />
    </div>
    <div class="flex-1">
      <form
        @submit.prevent="handleSubmit"
        class="bg-mist-900 p-4 flex rounded-xl gap-4 items-center">
        <input
          v-model="taskName"
          type="text"
          class="flex-1 min-w-50 h-12 px-4 text-[16px] text-white placeholder:text-white font-semibold placeholder:font-semibold bg-mist-700 rounded"
          placeholder="Title" />
        <input
          v-model="taskDueDate"
          type="date"
          class="w-44 h-12 px-4 text-[16px] text-white placeholder:text-white font-semibold placeholder:font-semibold bg-mist-700 rounded" />
        <div class="flex items-center gap-4 bg-mist-700 h-12 px-4 rounded">
          <span class="text-white font-semibold text-sm">Priority:</span>
          <div class="flex gap-3">
            <label v-for="p in ['Low', 'Medium', 'High']" :key="p" class="flex items-center gap-2 text-white font-semibold cursor-pointer select-none">
              <input
                type="radio"
                name="priority"
                :value="p"
                v-model="taskPriority"
                class="appearance-none w-4 h-4 rounded-full bg-white/10 checked:bg-[radial-gradient(var(--color-mist-900)_35%,var(--color-mist-400)_40%)] transition-all duration-150" />
              <span class="text-sm">{{ p }}</span>
            </label>
          </div>
        </div>
        <button
          type="submit"
          class="h-12 px-4 text-[16px] bg-mist-700 text-white font-bold hover:bg-mist-500 rounded">
          Add
        </button>
      </form>
    </div>
  </div>
</template>
