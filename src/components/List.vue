<script setup lang="ts">
interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

const { todos } = defineProps<{ todos: Todo[] }>();
const emit = defineEmits<{ deleteTodo: [number] }>();
</script>

<template>
  <ul>
    <li
      v-for="todo in todos"
      :key="todo.id"
    >
      <div>
        <h2 :class="{ todoDone: todo.completed }">{{ todo.title }}</h2>
        <input
          type="checkbox"
          v-model="todo.completed"
        />
        <button
          type="button"
          @click="emit('deleteTodo', todo.id)"
        >
          Delete this todo
        </button>
      </div>
    </li>
  </ul>
</template>

<style scoped>
.todoDone {
  text-decoration: line-through;
}
</style>
