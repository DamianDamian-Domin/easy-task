<template>
    <div class="task bg-white p-2 mb-2 rounded shadow-sm " :title="task.createdAt.toLocaleDateString()">
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