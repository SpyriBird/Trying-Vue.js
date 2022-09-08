<script setup lang="ts">
defineProps({
  todo: String
})
defineEmits(['remove-me'])
</script>

<template>
  {{todo}}
  <button @click="$emit('remove-me')"> - </button>
</template>