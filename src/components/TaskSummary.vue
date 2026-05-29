<script setup>
import { computed } from "vue";
const props = defineProps({
  tasks: Array,
});

const emit = defineEmits([
  "clear-completed",
  "clear-all",
  "select-all",
  "deselect-all",
]);

const totalTasks = computed(() => props.tasks.length);
const incompleteTasks = computed(
  () => props.tasks.filter((task) => !task.isChecked).length,
);
const completedTasks = computed(() => totalTasks.value - incompleteTasks.value);

const clearCompleted = () => emit("clear-completed");

const clearAll = () => emit("clear-all");

const selectAll = () => emit("select-all");

const DeselectAll = () => emit("deselect-all");

const allSelected = computed(
  () => props.tasks.length > 0 && props.tasks.every((task) => task.isChecked),
);
</script>

<template>
  <div
    class="flex flex-wrap w-auto items-center gap-3 bg-mist-700 text-white font-semibold h-auto min-h-12 px-4 py-2 rounded">
    <span>Incomplete: {{ incompleteTasks }}</span>
    <span>Complete: {{ completedTasks }}</span>
    <span>Total: {{ totalTasks }}</span>
    <button
      @click="clearCompleted"
      class="h-8 w-37 bg-mist-900 text-white font-bold hover:bg-mist-500 rounded">
      Clear Completed
    </button>
    <button
      @click="clearAll"
      class="h-8 w-21 bg-mist-900 text-white font-bold hover:bg-mist-500 rounded">
      Clear All
    </button>
    <button
      v-if="allSelected"
      @click="DeselectAll"
      class="h-8 w-29 bg-mist-900 text-white font-bold hover:bg-mist-500 rounded">
      Deselect All
    </button>
    <button
      v-else
      @click="selectAll"
      class="h-8 w-22 bg-mist-900 text-white font-bold hover:bg-mist-500 rounded">
      Select All
    </button>
  </div>
</template>
