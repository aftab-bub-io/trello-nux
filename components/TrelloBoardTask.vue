<script setup lang="ts">
import type { Task } from "@/types"

defineProps<{
    task: Task
}>();
</script>

<template>
    <div :title="task.createdAt.toLocaleDateString()"
        class="bg-white p-2 mb-2 text-gray-700 rounded shadow-md max-w-[250px] flex justify-start gap-2 items-center">
    <DragHandle />
    <span>
        {{ task.title }}
    </span>
    </div>
</template>