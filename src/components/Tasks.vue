<script setup>
import Task from './Task.vue'

defineProps({
  tasks: Array
})
defineEmits(['delete-task', 'toggle-reminder'])
</script>

<template>
  <div :key="task.id" v-for="task in tasks">
    <Task @toggle-reminder="$emit('toggle-reminder', task.id)" @delete-task="$emit('delete-task', task.id)"
      :task="task" />
  </div>
</template>