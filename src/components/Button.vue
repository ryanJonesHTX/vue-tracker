<script setup>
defineProps({
  text: String,
  color: String,
})

const emit = defineEmits(['btn-click'])

function onClick() {
  emit('btn-click')
}

</script>

<template>
  <button @click="onClick()" :style="{ background: color }" class="btn">{{ text }}</button>
</template>