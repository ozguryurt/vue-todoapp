<script setup lang="ts">
import type { TodoType } from '../types/TodoType';
defineProps<{ todo: TodoType }>();

const toggleDone = (todo: { done: boolean }) => {
    todo.done = !todo.done;
};
</script>

<template>
    <div @click="toggleDone(todo)"
        class="w-full lg:w-[32rem] bg-slate-100 rounded-md p-2 shadow flex justify-between items-center gap-3 cursor-pointer"
        :class="{ 'opacity-50': todo.done }">
        <h1 class="text-base font-normal" :class="{ 'line-through': todo.done }">{{ todo.content }}</h1>
    </div>
</template>

<style scoped></style>