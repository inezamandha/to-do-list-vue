<template>
  <div class="container">
    <TodoBoard :todos="todos" @add="addTodo" @remove="removeTodo" @toggle="changeStatusTodo" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import TodoBoard from './components/ToDoBoard.vue'

const todos = ref([])

function addTodo(todo) {
  todos.value.push(todo)
}

function removeTodo(index) {
  todos.value.splice(index, 1)
}

function changeStatusTodo(index) {
  todos.value[index].completed = !todos.value[index].completed
}
</script>

<style>
body {
  margin: 0;
  font-family: sans-serif;
}

.container {
  max-width: 500px;
  margin: 40px auto;
  padding: 1rem;
}
</style>
