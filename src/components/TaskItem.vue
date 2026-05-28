<script setup>
import { ref } from "vue";
const props = defineProps({
  task: Object,
});
const emit = defineEmits(["task-remove", "edit-task", "task-complete"]);

const editTask = () => {
  emit("edit-task", props.task.id);
};

const remove = () => {
  emit("task-remove", props.task.id);
};

const completeTask = () => {
  emit("task-complete", props.task.id);
};
</script>

<template>
  <div
    class="flex justify-between p-4 rounded cursor-pointer transition-all bg-mist-700 text-white hover:bg-mist-500">
    <div class="flex items-center gap-3">
      <input
        type="checkbox"
        :checked="task.isChecked"
        @change="completeTask"
        class="relative peer h-5 w-5 shrink-0 transition-all cursor-pointer appearance-none rounded shadow hover:shadow-md bg-mist-400 checked:bg-mist-900 checked:before:content-['\2714'] checked:before:absolute checked:before:inset-0 checked:before:flex checked:before:items-center checked:before:justify-center checked:before:text-white checked:before:text-sm" />
      <div class="flex flex-col">
        <label
          class="peer-checked:line-through peer-checked:text-mist-400 max-w-full font-semibold">
          {{ task.name }}
        </label>
        <div class="flex gap-2 text-xs text-mist-300">
          <span v-if="task.dueDate">Due: {{ task.dueDate }}</span>
          <span v-if="task.priority">Priority: {{ task.priority }}</span>
        </div>
      </div>
    </div>
    <div class="flex items-center gap-3">
      <button
        @click="editTask"
        class="px-3 py-2 rounded bg-mist-900 text-white hover:bg-mist-700">
        Edit
      </button>
      <button
        @click="remove"
        class="px-3 py-2 rounded bg-mist-900 text-white hover:bg-mist-700">
        X
      </button>
    </div>
  </div>
</template>
