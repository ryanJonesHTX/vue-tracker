<script setup>
import Button from './Button.vue'
defineProps({
  title: {
    type: String,
    required: true
  }
})
</script>

<template>
  <header>
    <h1>{{ title }}</h1>
    <Button text="Add Task" color="green" />
  </header>
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>