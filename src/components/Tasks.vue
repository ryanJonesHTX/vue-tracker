<script setup>
import Task from './Task.vue'

defineProps({
  tasks: Array
})
defineEmits(['delete-task'])
</script>

<template>
  <div :key="task.id" v-for="task in tasks">
    <Task @delete-task="$emit('delete-task', task.id)" :task="task" />
  </div>
</template>