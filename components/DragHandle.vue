<template>
    <span v-if="color === 'red'" class="drag-handle cursor-move"> 🔸 </span>
    <span v-else-if="color === 'blue'" class="drag-handle cursor-move"> 🔹 </span>
</template>

<script setup lang="ts">

defineProps<{
    color: String;
}>()

</script>