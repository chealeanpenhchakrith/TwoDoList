<template>
  <h1>Hello Rith !</h1>
  <form @submit.prevent="addTask">
    <fieldset>
      <legend>To Do List</legend>
      <label>
        Enter a task :
        <input type="text" v-model="currentTask" placeholder="Cook food.."/>
      </label>
      <button :disabled="currentTask.length === 0">Add Task</button>
    </fieldset>
  </form>
  <div v-if="taskList.length === 0">
    <h3>No Task to display</h3>
  </div>
  <div v-else>
    <ul>
      <li v-for="task in sortedToDo()" :key="task.date" :class="{completed: task.completed}">
        <label>
          <input type="checkbox" v-model="task.completed"/>
          <span>{{ task.title }}</span>
        </label>
      </li>
    </ul>
    <label>
      <input type="checkbox" v-model="hideCompleted"> 
      Masquer les tâches complétées
    </label>
  </div>
</template>

<script setup>
import { ref } from "vue";

const taskList = ref([]);

const currentTask = ref("");

const hideCompleted = ref(false)

const addTask = () => {
  taskList.value.push({
    title: currentTask.value,
    completed: false,
    data: Date.now()
  })
  currentTask.value = ''
};

const sortedToDo = () => {
  const sortedToDos = taskList.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)
  if (hideCompleted.value === true) {
    return sortedToDos.filter(t => t.completed === false)
  }
  return sortedToDos
}
</script>

<style scoped>
li {
  list-style-type: none;
}

.completed {
  opacity: .5;
  text-decoration: line-through;
}
</style>
