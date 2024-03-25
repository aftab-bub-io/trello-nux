<script setup lang="ts">
import type { Column, Task } from "@/types"
import { nanoid } from "nanoid"
import draggable from "vuedraggable";

const columns = ref<Column[]>(
    [
        {
            title: "Backlog",
            id: nanoid(),
            tasks: [
                {
                    title: "Create marketing landing page",
                    createdAt: new Date(),
                    id: nanoid(),
                },
                {
                    title: "Develop cool new feature",
                    createdAt: new Date(),
                    id: nanoid(),
                },
                { title: "Fix page nav bug", createdAt: new Date(), id: nanoid() },
            ],
        },
        { title: "Selected for Dev", id: nanoid(), tasks: [] },
        { title: "In Progress", id: nanoid(), tasks: [] },
        { title: "QA", id: nanoid(), tasks: [] },
        { title: "Complete", id: nanoid(), tasks: [] },
    ],
)
</script>

<template>
    <div>
        <draggable v-model="columns" group="columns" handle=".drag-handle" :animation="150" item-key="id"
            class="flex gap-4 overflow-x-auto items-start">
            <template #item="{ element: column }: { element: Column }">
                <div class="bg-gray-200 p-5 min-w-[250px] rounded">
                    <header class="text-gray-800 font-bold mb-4 flex gap-2 justify-flex-start items-center">
                        <DragHandle />
                        {{ column.title }}
                    </header>
                    <draggable v-model="column.tasks" group="tasks" handle=".drag-handle" item-key="id"
                        :animation="150">
                        <template #item="{element: task}: {element: Task}">
                            <TrelloBoardTask :task="task" />
                        </template>
                    </draggable>
                    <footer>
                        <button class="text-gray-500">+ Add a Card</button>
                    </footer>
                </div>
            </template>
        </draggable>
    </div>
    <!-- <pre>{{ columns }}</pre> -->
</template>
