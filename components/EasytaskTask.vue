<template>
    <div 
    class="bg-white p-2 mb-2 rounded shadow-sm flex gap-2 max-w-[250px] focus:bg-gray-400 hover:cursor-pointer focus-visible:outline-none "
    @focus="focused=true"
    @blur="focused=false"
    tabindex="0" 
    >
        <DragHandle color="blue"></DragHandle>
        <span> {{ task.title }} </span>
    </div>
</template>

<script setup lang="ts">
import type { Task } from '~/types';
const props = defineProps<{
    task: Task;
}>()
const emit = defineEmits<{
    (e: "delete", payload: string): void
}>()

const focused = ref(false)
onKeyStroke("Backspace", (e) => {
    if(focused.value) {
        emit("delete", props.task.id)
    }
})

</script>
