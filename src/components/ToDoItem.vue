<template>
  <li class="item">
    <label class="label">
      <input type="checkbox" :checked="todo.completed" @change="$emit('toggle')" />
      <div class="text-container">
        <span :class="{ done: todo.completed }" class="text">
          {{ todo.text }}
        </span>
        <p v-if="todo.due" class="due">
          <i class="fas fa-calendar-alt"></i> {{ formatDate(todo.due) }}
        </p>
      </div>
    </label>
    <button @click="$emit('remove')" class="remove">×</button>
  </li>
</template>

<script setup>
defineProps({
  todo: {
    type: Object,
    required: true,
  },
})

function formatDate(dateStr) {
  const d = new Date(dateStr)
  return d.toLocaleDateString('en-ID', {
    year: 'numeric',
    month: 'short',
    day: 'numeric',
  })
}
</script>

<style scoped>
.item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: white;
  border: 1px solid #ddd;
  padding: 0.75rem 1rem;
  border-radius: 0.75rem;
  font-size: 1rem;
}

.label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  flex: 1;
  padding-right: 10px;
}

input[type='checkbox'] {
  width: 1rem;
  height: 1rem;
  cursor: pointer;
  accent-color: black;
}

.done {
  text-decoration: line-through;
  color: #888;
}

.text-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 90%;
  gap: 20px;
}

.text {
  font-size: 14px;
  text-align: start;
}

.due {
  font-size: 12px;
  min-width: 90px;;
  text-align: end;
}

button {
  background: none;
  border: none;
  font-size: 1.25rem;
  cursor: pointer;
  color: #444;
}

.fas.fa-calendar-alt {
  margin-right: 4px;
  color: #444;
}

@media (min-width: 480px) {
  .text {
    font-size: 16px;
  }

  .due {
    font-size: 14px;
    min-width: 125px;
  }
}
</style>
