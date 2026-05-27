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

    <div class="mt-6 grid gap-3">
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @task-remove="removeTask"
      />
    </div>
  </div>
</template>
