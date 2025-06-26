<template>
  <div class="board">
    <h1>To-Do List</h1>

    <form @submit.prevent="onAdd" class="form">
      <input v-model="newTodo" type="text" placeholder="Add new task" required />
      <input v-model="dueDate" type="date" required />
      <button type="submit">
        <span class="mobile-label">Add</span>
        <span class="desktop-label">+</span>
      </button>
    </form>

    <div v-if="todos.length === 0" class="empty">No tasks yet. Add something!</div>

    <ul v-else class="list">
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :todo="todo"
        @toggle="$emit('toggle', index)"
        @remove="$emit('remove', index)"
      />
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import TodoItem from './ToDoItem.vue'

const props = defineProps({
  todos: Array,
})

const emit = defineEmits(['add', 'remove', 'toggle'])

const newTodo = ref('')
const dueDate = ref('')

function onAdd() {
  if (!newTodo.value.trim() || !dueDate.value) return

  emit('add', {
    text: newTodo.value,
    completed: false,
    due: dueDate.value,
  })

  newTodo.value = ''
  dueDate.value = ''
}
</script>

<style scoped>
.board {
  background: white;
  padding: 1rem;
}

h1 {
  font-size: 1.5rem;
  font-weight: 600;
  text-align: left;
  margin-bottom: 1rem;
}

.form {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
  border-bottom: 1px solid #ccc;
  padding-bottom: 0.5rem;
}

input[type='text'],
input[type='date'] {
  flex: 1 1 100%;
  padding: 0.5rem;
  font-size: 1rem;
  border: none;
  border-radius: 0.5rem;
  box-sizing: border-box;
  background-color: #f9f9f9;

  height: 44px;
}

input[type='text']:focus,
input[type='date']:focus {
  outline: none;
  background-color: #f9f9f9;
}

button[type='submit'] {
  background: #444;
  color: white;
  border: none;
  font-size: 1rem;
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  cursor: pointer;
  flex: 1 1 100%;
  text-align: center;
}

.list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 0.75rem;
}

.empty {
  text-align: center;
  color: #888;
  font-size: 1rem;
  padding: 1.5rem 0;
  border: 1px solid #ddd;
  border-radius: 0.75rem;
  background-color: #fafafa;
}

.mobile-label {
  display: inline;
  font-size: 14px;
}

.desktop-label {
  display: none;
}

@media (min-width: 480px) {
  .form {
    flex-wrap: nowrap;
  }

  input[type='text'],
  input[type='date'] {
    flex: 1 1 auto;
  }

  button[type='submit'] {
    width: 2.5rem;
    height: 2.5rem;
    padding: 0;
    font-size: 1.25rem;
    border-radius: 25%;
    flex: 0 0 auto;
    text-align: center;
  }

  .mobile-label {
    display: none;
  }
  .desktop-label {
    display: inline;
  }
}
</style>
