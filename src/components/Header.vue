<script setup>
import { ref } from "vue";

const inputValue = ref("");
const tasks = ref([]);

function newElement() {
  if (inputValue.value.trim() === "") {
    alert("Please enter a task.");
    return;
  }
  tasks.value.push({ text: inputValue.value.trim(), checked: false });
  inputValue.value = "";
}

function removeTask(index) {
  tasks.value.splice(index, 1);
}

function toggleTask(index) {
  tasks.value[index].checked = !tasks.value[index].checked;
}
</script>

<template>
  <div class="bg-blue-950 p-[30px_40px] flex flex-col items-center justify-center gap-4 text-center">
    <h1 class="text-4xl font-bold text-blue-300">Task Manager</h1>
    <input
      class="w-full max-w-2xl p-2.5 text-[16px] text-black outline-none bg-blue-500 rounded"
      v-model="inputValue"
      type="text"
      placeholder="Enter task here..."
      @keyup.enter="newElement"
    />
    <span class="w-20 max-w-2xl p-2.5 text-[20px] bg-blue-400 text-blue-950 transition-all duration-300 hover:bg-blue-200 cursor-pointer rounded" @click="newElement">Add</span>
  </div>

  <ul class = "w-full">
    <li
      v-for="(task, index) in tasks"
      :key="index"
      @click="toggleTask(index)"
      :class="[
        'relative cursor-pointer text-[18px] py-3 pr-12 pl-12 transition-all duration-200 select-none',
        'bg-slate-800 even:bg-slate-700 hover:bg-slate-600 hover:text-black',
        task.checked ? 'line-through before:content-[\'\'] before:absolute before:border-white before:border-solid before:border-r-2 before:border-b-2 before:top-3.5 before:left-5 before:rotate-45 before:h-3.75 before:w-1.75' : ''
      ]"
    >
      {{ task.text }}
      <span 
    class="absolute right-0 top-0 p-3 hover:bg-slate-300 hover:text-black transition-colors duration-200"
    @click.stop="removeTask(index)">&#215;</span>
    </li>
  </ul>
</template>
