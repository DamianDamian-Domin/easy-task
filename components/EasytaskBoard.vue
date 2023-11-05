<template>
    <div class="flex py-4 items-start overflow-x-auto gap-4">
        <draggable 
        v-model="columns" 
        group="columns" 
        item-key="id" 
        :animation="150"
        handle=".drag-handle"
        class="flex flex-row gap-4 items-start" 
        >
            <template #item="{element: column}: {element: Column}">
                <div class="column bg-gray-200 p-5 rounded min-w-[250px]">
                    <header class="font-bold mb-4">
                        <DragHandle color="red"></DragHandle>
                        <input 
                        class="title-input bg-transparent focus:bg-white rounded px-1 w-4/5 focus:outline-dashed"
                        @keyup.enter="($event.target as HTMLInputElement).blur()"
                        @keydown.backspace="column.title === '' ? columns = columns.filter(c => c.id !== column.id) : null"
                        type="text"
                        v-model="column.title"
                        />
                    </header>
                    <draggable 
                    v-model="column.tasks" 
                    :group="{name: 'tasks', pull: alt ? 'clone' : true}" 
                    item-key="id" 
                    :animation="150"
                    handle=".drag-handle"
                    class="task"
                    >
                        <template #item="{element: task}: {element: Task}">
                            <EasytaskTask 
                            :task="task" 
                            @delete="column.tasks = column.tasks.filter(task => task.id !== $event)"></EasytaskTask>
                        </template>
                    </draggable>
                    <footer>
                        <NewTask @add="column.tasks.push($event)"></NewTask>
                    </footer>
                </div>
            </template>
        </draggable>
        <button 
        @click="createColumn()"
        class="bg-gray-200 whitespace-nowrap p-2 rounded opacity-50"
        >
        + New column
        </button>
    </div>
</template>

<script setup lang="ts">
import type { Column, Task } from '~~/types'
import { nanoid } from 'nanoid'
import draggable from "vuedraggable"

const alt = useKeyModifier("Alt")
const columns = useLocalStorage<Column[]>('EasyTask', [
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

function createColumn() {
    const column: Column = {
        id: nanoid(),
        title: "",
        tasks: []
    };
    columns.value.push(column)
    nextTick(() => {
        (document.querySelector(".column:last-of-type .title-input") as HTMLInputElement).focus()
    })
}

</script>

<style>
.task > .sortable-drag  {
    @apply bg-gray-400 !important;
    transform: translateX(180px) rotate(45deg);
    transform: skewY(5deg);
}


</style>