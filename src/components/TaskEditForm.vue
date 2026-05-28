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
    class="bg-mist-700 p-4 flex rounded items-center gap-3">
    <input
      v-model="draftTaskName"
      type="text"
      class="flex-1 pl-2 py-1 ml-6 text-[16px] text-white font-semibold placeholder:font-semibold placeholder:text-mist-300 outline-none bg-mist-900 rounded"
      placeholder="Edit task..." />
    <button
      type="submit"
      class="px-3 py-1 rounded bg-mist-900 text-white hover:bg-mist-700"">
      Save
    </button>
    <button
      type="button"
      @click="handleCancel"
      class="px-3 py-1 rounded bg-mist-900 text-white hover:bg-mist-700"">
      Cancel
    </button>
  </form>
</template>
