<script setup>
import { ref } from "vue";

const props = defineProps({
  task: Object,
});

const draftTaskName = ref(props.task?.name || "");
const draftTaskDueDate = ref(props.task?.dueDate || "");
const draftTaskPriority = ref(props.task?.priority ?? "");
const emit = defineEmits(["task-changed", "cancel"]);

const handleSave = () => {
  if (!draftTaskName.value.trim()) {
    alert(
      "Error: Editing a task cannot result in a blank name! Please delete the task instead.",
    );
    return;
  }
  emit(
    "task-changed",
    props.task.id,
    draftTaskName.value,
    draftTaskDueDate.value,
    draftTaskPriority.value,
  );
};

const handleCancel = () => {
  emit("cancel");
};
</script>

<template>
  <form
    @submit.prevent="handleSave"
    class="bg-mist-700 px-5 py-4 flex rounded items-center gap-3">
    <input
      v-model="draftTaskName"
      type="text"
      class="flex-1 pl-3 py-2 ml-6 text-[16px] text-white font-semibold placeholder:font-semibold placeholder:text-mist-300 outline-none bg-mist-900 rounded"
      placeholder="Edit task..." />
    <input
      v-model="draftTaskDueDate"
      type="date"
      class="py-2 flex-initial px-4 text-[16px] text-white placeholder:text-white font-semibold placeholder:font-semibold bg-mist-900 rounded" />
    <input
      v-model="draftTaskPriority"
      type="text"
      class="w-8 p-2 pl-2.5 flex-initial text-[16px] text-white placeholder:text-white font-semibold placeholder:font-semibold bg-mist-900 rounded" />
    <button
      type="submit"
      class="px-3 py-2 rounded bg-mist-900 text-white hover:bg-mist-700">
      Save
    </button>
    <button
      type="button"
      @click="handleCancel"
      class="px-3 py-2 rounded bg-mist-900 text-white hover:bg-mist-700">
      Cancel
    </button>
  </form>
</template>
