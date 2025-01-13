<script setup lang="ts">
import { ref } from 'vue'
import type { TodoType } from '../types/TodoType'

const props = defineProps<{ todos: TodoType[] }>()
const emit = defineEmits(['update:todos'])

const todoContent = ref("")

const addTodo = () => {
    if (todoContent.value.trim() === '') return alert("Boş alan bırakmayın.")

    const newTodo: TodoType = {
        id: props.todos.length > 0 ? Math.max(...props.todos.map(t => t.id)) + 1 : 1,
        content: todoContent.value,
        done: false
    }

    emit('update:todos', [...props.todos, newTodo])

    todoContent.value = ''
}
</script>

<template>
    <div class="w-full lg:w-[32rem] bg-slate-100 rounded-md p-2 shadow flex flex-col justify-center items-center gap-1">
        <input v-model="todoContent" type="text" class="w-full bg-white rounded-md text-base p-2"
            placeholder="Yeni todo oluştur...">
        <button class="w-full bg-blue-500 hover:bg-blue-600 transition-colors text-white rounded-md text-base p-2"
            @click="addTodo">
            Oluştur
        </button>
    </div>
</template>