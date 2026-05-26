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
  tasks.value.splice(index, 1);
}
</script>

<template>
  <div id="myDiv" class="header">
    <h1>Task Manager</h1>
    <input
      v-model="inputValue"
      type="text"
      placeholder="Enter here..."
      @keyup.enter="newElement"
    />
    <span class="addBtm" @click="newElement">Add</span>
  </div>

  <ul id="myUL">
    <li
      v-for="(task, index) in tasks"
      :key="index"
      :class="{ checked: task.checked }"
      @click="toggleTask(index)"
    >
      {{ task.text }}
      <span class="close" @click.stop="removeTask(index)">&#215;</span>
    </li>
  </ul>
</template>

<style scoped>
ul {
  margin: 0;
  padding: 0;
}

ul li {
  cursor: pointer;
  position: relative;
  background: var(--vt-c-text-dark-2);
  font-size: 18px;
  transition: 0.2s;
}

ul li:nth-child(odd) {
  background: var(--vt-c-text-light-2);
}

ul li:hover {
  background: #ddd;
}

ul li:checked {
  background: #888;
  color: #fff;
  text-decoration: line-through;
}

ul li.checked::before {
  content: "";
  position: absolute;
  border-color: #fff;
  border-style: solid;
  border-width: 0 2px 2px 0;
  top: 10px;
  left: 16px;
  transform: rotate(45deg);
  height: 15px;
  width: 7px;
}

.close {
  position: absolute;
  right: 0;
  top: 0;
  padding: 12px;
}

.close:hover {
  background-color: var(--color-background-mute);
  color: black;
}

.header {
  background-color: var(--vt-c-indigo);
  padding: 30px 40px;
  color: var(--vt-c-white);
  text-align: center;
}

input {
  margin: 0;
  border: none;
  border-radius: 0;
  width: 75%;
  padding: 10px;
  float: left;
  font-size: 16px;
}
.addBtn {
    cursor: pointer;
  padding: 10px;
  width: 25%;
  float: left;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
  transition: 0.3s;
  border-radius: 0;
}

.addBtn:hover {
  background-color: #bbb;
}
</style>
