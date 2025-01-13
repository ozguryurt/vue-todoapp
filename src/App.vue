<script setup lang="ts">
import { ref } from 'vue'
import type { TodoType } from './types/TodoType'

import Todo from './components/Todo.vue'
import NewTodo from './components/NewTodo.vue'

const todos = ref<TodoType[]>([
  {
    id: 1,
    content: "Todo #1Todo #1Todo #1Todo #1Todo #1Todo #1",
    done: true,
  },
  {
    id: 2,
    content: "Todo #2",
    done: false,
  },
  {
    id: 3,
    content: "Todo #3",
    done: false,
  },
])
</script>

<template>
  <div class="min-h-screen flex flex-col justify-start items-center gap-3 p-5">
    <span class="text-3xl font-bold">Vue Todo App</span>
    <NewTodo v-model:todos="todos" />
    <span class="text-base font-medium" v-if="todos.length === 0">Todo bulunamadı.</span>
    <Todo v-for="todo in todos" :key="todo.id" :todo="todo" v-model:todos="todos" />
  </div>
</template>