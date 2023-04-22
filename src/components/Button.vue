<script setup>
defineProps: ({
  text: String,
  color: String,
}
)

</script>

<template>
  <button :style="{ background: color }" class="btn">{{ text }}</button>
</template>