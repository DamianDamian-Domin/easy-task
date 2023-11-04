<template>
    <div>
        <draggable 
        v-model="columns" 
        group="columns" 
        item-key="id" 
        :animation="150"
        handle=".drag-handle"
        class="flex flex-row gap-4 overflow-x-auto items-start" 
        >
            <template #item="{element: column}: {element: Column}">
                <div class="column bg-gray-200 p-5 rounded min-w-[250px]">
                    <header class="font-bold mb-4">
                        <DragHandle color="red"></DragHandle>
                        {{ column.title }}
                    </header>
                    <draggable 
                    v-model="column.tasks" 
                    group="tasks" 
                    item-key="id" 
                    :animation="150"
                    handle=".drag-handle"
                    >
                        <template #item="{element: task}: {element: Task}">
                            <EasytaskTask :task="task"></EasytaskTask>
                        </template>
                    </draggable>
                    <footer>
                        <button class=" text-gray-500">+ Add a Card</button>
                    </footer>
                </div>
            </template>
        </draggable>
    </div>
</template>

<script setup lang="ts">
import type { Column, Task } from '~~/types'
import { nanoid } from 'nanoid'
import draggable from "vuedraggable"
const columns = ref<Column[]>([
    {
        id: nanoid(),
        title: "Backlog",
        tasks: [
            {
                id: nanoid(),
                title: "Create marketing landing page",
                createdAt: new Date()
            },
            {
                id: nanoid(),
                title: "Add authentication and authorization",
                createdAt: new Date()
            },
            {
                id: nanoid(),
                title: "Create color palette",
                createdAt: new Date()
            }
        ]
    },
    {
        id: nanoid(),
        title: "Selected for dev",
        tasks: [
            {
                id: nanoid(),
                title: "Add firebase authentication",
                createdAt: new Date()
            },
            {
                id: nanoid(),
                title: "Refactor code",
                createdAt: new Date()
            }
        ]
    },
    {
        id: nanoid(),
        title: "In progress",
        tasks: []
    },
    {
        id: nanoid(),
        title: "QA",
        tasks: []
    },
    {
        id: nanoid(),
        title: "Complete",
        tasks: [
            {
                id: nanoid(),
                title: "My first task",
                createdAt: new Date()
            }
        ]
    }
])

</script>

<style scoped>

</style>