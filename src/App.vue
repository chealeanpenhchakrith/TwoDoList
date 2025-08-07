<template>
  <h1>To Do List</h1>
  <label>
    Enter a task :
    <input type="text" v-model="currentTask" @keyup.enter="addTask"/>
  </label>
  <button v-on:click="addTask">Add Task</button>
  <div v-if="taskList.length === 0">
    <h3>No Task to display</h3>
  </div>
  <div v-else>
    <ul>
      <li v-for="task in taskList" :key="task"> 
        <label>
          <input type="checkbox">
          <span>{{ task }}</span>
        </label>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from "vue";

const taskList = ref([]);

const currentTask = ref('');

const addTask = () => {
  taskList.value.push(currentTask.value);
  currentTask.value = '';
};
</script>

<style scoped>
li {
  list-style-type: none;
}

input[type="checkbox"]:checked + span {
    text-decoration: line-through;
}
</style>

