<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'

let tasks = ref([
  {
    id: 1,
    text: 'Doctors Appointment',
    day: 'March 1st at 2:30pm',
    reminder: false,
  },
  {
    id: 2,
    text: 'Last day at PINE',
    day: 'April 28th',
    reminder: true,
  },
  {
    id: 3,
    text: 'First day at Unleaded',
    day: 'May 1st at 7:00am',
    reminder: true,
  }
])

const deleteTask = (id) => {
  if (confirm('Are you sure?')) {
    tasks.value = tasks.value.filter((task) => task.id !== id)
    console.log(tasks)
  }
}

</script>

<template>
  <header>
    <div class="container">
      <Header title="Task Tracker" />
      <Tasks @delete-task="deleteTask" :tasks="tasks" />
    </div>
  </header>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

header {
  line-height: 1.5;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
