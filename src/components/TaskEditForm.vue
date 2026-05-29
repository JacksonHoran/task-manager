<script setup>
import { ref } from "vue";

const props = defineProps({
  task: Object,
});

const draftTaskName = ref(props.task?.name || "");
const draftTaskDueDate = ref(props.task?.dueDate || "");
const draftTaskPriority = ref(props.task?.priority || "Low");
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
    class="bg-mist-700 px-5 py-4 flex flex-wrap rounded items-center gap-3">
    <input
      v-model="draftTaskName"
      type="text"
      class="flex-1 min-w-37.5 pl-3 py-2 ml-6 text-[16px] text-white font-semibold placeholder:font-semibold placeholder:text-mist-300 outline-none bg-mist-900 rounded"
      placeholder="Edit task..." />
    <input
      v-model="draftTaskDueDate"
      type="date"
      class="py-2 w-44 px-4 text-[16px] text-white placeholder:text-white font-semibold placeholder:font-semibold bg-mist-900 rounded" />
    <div class="flex items-center gap-3 bg-mist-900 h-10 px-3 rounded">
      <span class="text-white font-semibold text-sm">Priority:</span>
      <div class="flex gap-2">
        <label
          v-for="p in ['Low', 'Medium', 'High']"
          :key="p"
          class="flex items-center gap-1.5 text-white font-semibold cursor-pointer select-none">
          <input
            type="radio"
            :name="'edit-priority-' + task.id"
            :value="p"
            v-model="draftTaskPriority"
            class="appearance-none w-4 h-4 rounded-full bg-white/10 checked:bg-[radial-gradient(var(--color-mist-900)_35%,var(--color-mist-400)_40%)] transition-all duration-150" />
          <span class="text-xs">{{ p }}</span>
        </label>
      </div>
    </div>
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
