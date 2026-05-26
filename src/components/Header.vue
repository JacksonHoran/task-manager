<script setup>
import { ref } from 'vue'

</script>

<template >
  <header class="header">
    <h1>Task Manager</h1>
    
    <form class = "input">
        <label> New Task:</label>
        <input type="text" id="newTask">
    </form>
  </header>
</template>

<style scoped>
.header{
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
    width: 100%;
    padding: 0.5rem 1rem;
    background-color: #f5f7fa;
}
.header h1{
    margin: 0;
    font-size: 2.25rem;
    font-weight: 700;
    color: #111827;
}

.input {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 1rem;
}
.input label {
    margin: 0;
    font-size: 2.25rem;
    font-weight: 700;
    color: #111827;

}

.input input{
    padding: 0.4rem 0.6rem;
    font-size: 1rem;
    background-color: #111827;
    color: #f5f7fa;
}
</style>