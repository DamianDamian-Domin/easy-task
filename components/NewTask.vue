<template>
    <div>
        <textarea 
        v-model="title" 
        @keydown.tab="createTask" 
        @keyup.enter="createTask" 
        class="textarea focus:p-2 bg-transparent focus:bg-white focus:shadow resize-none rounded w-full border-" 
        :class="{
            'h-7': !focused,
            'h-20': focused
        }"
        @focus="focused = true"
        @blur="focused = false; title = ''"
        :placeholder="!focused ? '+ Add a card' : 'Enter a title for this card'"
        >   
        </textarea>
    </div>
</template>

<script setup lang="ts">
import type { Task } from '~/types';
import { nanoid } from 'nanoid';

const emit = defineEmits<{
    (e: "add", payload: Task): void;
}>()

const focused = ref(false);
const title = ref("")

function createTask(e: Event)   {
    if (title.value.trim()) {
        e.preventDefault();
        emit("add", {
            id: nanoid(),
            title: title.value.trim(),
            createdAt: new Date(),
        } as Task)
    }
    title.value = ""

}

</script>

<style scoped>
.textarea {
    outline: none !important;
}
</style>