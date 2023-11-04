<template>
    <div class="bg-white p-2 mb-2 rounded shadow-sm flex gap-2 max-w-[250px] " :title="task.createdAt.toLocaleDateString()">
        <DragHandle color="blue"></DragHandle>
        <span> {{ task.title }} </span>
    </div>
</template>

<script setup lang="ts">
import type { Task } from '~/types';
defineProps<{
    task: Task;
}>()

</script>

<style scoped>

</style>