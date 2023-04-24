<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

const fetchTasks = async () => {
  const res = await fetch('api/tasks')

  const data = await res.json()

  return data
}

const fetchTask = async (id) => {
  const res = await fetch(`api/tasks/${id}`)

  const data = await res.json()

  return data
}

let tasks = ref([])
fetchTasks().then(data => {
  tasks.value = data
})

let showAddTask = ref(false)

const addTask = async (task) => {
  const res = await fetch('/api/tasks', {
    method: 'POST',
    headers: {
      'Content-type': 'application/json',
    },
    body: JSON.stringify(task)
  })

  const data = await res.json()

  tasks.value = [...tasks.value, data]
}

const deleteTask = async (id) => {
  if (confirm('Are you sure?')) {
    const res = await fetch(`api/tasks/${id}`, {
      method: 'DELETE'
    })

    res.status === 200 ? (tasks.value = tasks.value.filter((task) => task.id !== id)) : alert('Error deleting task')


  }
}

const toggleReminder = async (id) => {
  const taskToToggle = await fetchTask(id)
  const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder }

  const res = await fetch(`api/tasks/${id}`, {
    method: 'PUT',
    headers: {
      'Content-type': 'application/json'
    },
    body: JSON.stringify(updTask)
  })

  const data = await res.json()

  tasks.value = tasks.value.map((task) => task.id === id ? { ...task, reminder: data.reminder } : task)
}

const toggleAddTask = () => {
  showAddTask.value = !showAddTask.value
}


</script>

<template>
  <header>
    <div class="container">
      <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask" />
      <div v-if="showAddTask">
        <AddTask @add-task="addTask" />
      </div>
      <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
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
