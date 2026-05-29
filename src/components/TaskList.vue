<script setup>
import { ref, onMounted, watch } from "vue";
import TaskForm from "./TaskForm.vue";
import TaskItem from "./TaskItem.vue";
import TaskEditForm from "./TaskEditForm.vue";

const tasksArr = ref([]);
const currentTask = ref(null);
const currentSort = ref("name");

onMounted(() => {
  const savedTasks = localStorage.getItem("tasks");
  if (savedTasks) {
    tasksArr.value = JSON.parse(savedTasks);
  }
});

watch(
  tasksArr,
  (newTasks) => {
    localStorage.setItem("tasks", JSON.stringify(newTasks));
  },
  { deep: true },
);

const addNewTask = (taskData) => {
  tasksArr.value.push({
    id: Date.now(),
    name: taskData.name,
    dueDate: taskData.dueDate,
    priority: taskData.priority,
    isChecked: false,
  });
};

const updateTask = (id, newName, newDueDate, newPriority) => {
  let index = tasksArr.value.findIndex((t) => t.id === id);
  if (index !== -1) {
    let task = tasksArr.value[index];
    task.name = newName;
    task.dueDate = newDueDate;
    task.priority = newPriority;
  }
  currentTask.value = null;
};

const removeTask = (id) => {
  tasksArr.value = tasksArr.value.filter((t) => t.id === id);
};

const startEdit = (id) => {
  currentTask.value = tasksArr.value.find((t) => t.id === id);
};

const markTaskComplete = (id) => {
  let task = tasksArr.value.find((t) => t.id === id);
  if (task) task.isChecked = !task.isChecked;
};
</script>

<template>
  <div>
    <TaskForm
      v-model:sortBy="currentSort"
      @task-added="addNewTask" />
    <div v-if="tasksArr.length > 0" class="mt-1 mx-4 grid gap-3">
      <template v-for="task in tasksArr" :key="task.id">
        <TaskEditForm
          v-if="currentTask && currentTask.id === task.id"
          :task="currentTask"
          @task-changed="updateTask"
          @cancel="currentTask = null" />
        <TaskItem
          v-else
          :task="task"
          @task-complete="markTaskComplete"
          @edit-task="startEdit"
          @task-remove="removeTask" />
      </template>
    </div>
    <div
      v-else
      class="mt-12 flex flex-col items-center justify-center text-center p-8 rounded-xl">
      <h3 class="mt-12 text-2xl font-bold text-slate-200">All caught up!</h3>
      <p class="text-slate-400 my-1 max-w-xs">
        No tasks remaining. Add a new task above to get started.
      </p>
    </div>
  </div>
</template>
