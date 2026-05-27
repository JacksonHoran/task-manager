<script setup>
import { ref } from "vue";
import TaskForm from "./TaskForm.vue";
import TaskItem from "./TaskItem.vue";

const tasks = ref([]);

const addNewTask = (taskName) => {
  tasks.value.push({
    id: Date.now(),
    name: taskName,
  });
};

const removeTask = (id) => {
  const index = tasks.value.findIndex((t) => t.id === id);
  if (index !== -1) tasks.value.splice(index, 1);
};
</script>

<template>
  <div class="">
    <TaskForm @task-added="addNewTask" />

    <div v-if="tasks.length > 0" class="mt-6 grid gap-3">
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @task-remove="removeTask"
      />
    </div>

    <div
      v-else
      class="mt-12 flex flex-col items-center justify-center text-center p-8 rounded-xl"
    >
      <h3 class="mt-12 text-2xl font-bold text-slate-200">All caught up!</h3>
      <p class="text-slate-400 my-1 max-w-xs">
        No tasks remaining. Add a new task above to get started.
      </p>
    </div>
  </div>
</template>
