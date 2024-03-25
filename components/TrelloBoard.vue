<script setup lang="ts">
import type { Column } from "@/types"
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
        <draggable v-model="columns" group="columns" item-key="id" class="flex gap-4 overflow-x-auto items-start">
            <template #item="{ element: column }: { element: Column }">
                <div class="bg-gray-200 p-5 min-w-[250px] rounded">
                    <header class="text-gray-800 font-bold mb-4">
                        {{ column.title }}
                    </header>
                    <TrelloBoardTask v-for="task in column.tasks" :task="task" />
                    <footer>
                        <button class="text-gray-500">+ Add a Card</button>
                    </footer>
                </div>
            </template>
        </draggable>
    </div>
    <!-- <pre>{{ columns }}</pre> -->
</template>
