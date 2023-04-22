<script setup>
defineProps({
  text: String,
  color: String,
})

function onClick() {
  console.log('click')
}

</script>

<template>
  <button @click="onClick()" :style="{ background: color }" class="btn">{{ text }}</button>
</template>