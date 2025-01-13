<script setup lang="ts">
import type { TodoType } from '../types/TodoType'

const props = defineProps<{ todo: TodoType, todos: TodoType[] }>()
const emit = defineEmits(['update:todos'])

const toggleDone = (todoId: number) => {
    const updatedTodos = props.todos.map(t => {
        if (t.id === todoId) return { ...t, done: !t.done }
        return t
    })
    emit('update:todos', updatedTodos)
}

const deleteTodo = (todoId: number) => {
    const updatedTodos = props.todos.filter(todo => todo.id !== todoId)
    emit('update:todos', updatedTodos)
}
</script>

<template>
    <div class="w-full lg:w-[32rem] relative bg-slate-100 rounded-md p-2 shadow flex justify-between items-center gap-3 cursor-pointer"
        :class="{ 'opacity-50': todo.done }">
        <h1 @click="toggleDone(todo.id)" class="text-base font-normal" :class="{ 'line-through': todo.done }">
            {{ todo.content }}
        </h1>
        <div @click.stop="deleteTodo(todo.id)"
            class="absolute -top-1 -right-1 text-xs bg-red-500 hover:bg-red-600 px-3 py-1 text-white rounded cursor-pointer">
            Sil
        </div>
    </div>
</template>