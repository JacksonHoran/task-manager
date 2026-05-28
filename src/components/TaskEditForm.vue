<script setup>
import { ref } from "vue";

const props = defineProps({
  task: Object,
});

const draftTaskName = ref(props.task?.name || "");
const emit = defineEmits(["task-changed", "cancel"]);

const handleSave = () => {
  if (!draftTaskName.value.trim()) {
    alert("Error: Invalid input provided!");
    return;
  }
  emit("task-changed", props.task.id, draftTaskName.value);
  draftTaskName.value = "";
};

const handleCancel = () => {
  draftTaskName.value = "";
  emit("cancel");
};
</script>

<template>
  <form
    @submit.prevent="handleSave"
    class="bg-mist-700 p-4 mx-60 flex rounded-xl items-center gap-3">
    <input
      v-model="draftTaskName"
      type="text"
      class="flex-1 h-12 px-4 text-[16px] text-white font-semibold placeholder:font-semibold placeholder:text-mist-300 outline-none bg-mist-900 rounded"
      placeholder="Edit task..." />
    <button
      type="submit"
      class="h-12 px-4 text-[16px] bg-mist-900 text-white font-bold hover:bg-mist-500 rounded">
      Save
    </button>
    <button
      type="button"
      @click="handleCancel"
      class="h-12 px-4 text-[16px] bg-mist-900 text-white font-bold hover:bg-mist-500 rounded">
      Cancel
    </button>
  </form>
</template>
