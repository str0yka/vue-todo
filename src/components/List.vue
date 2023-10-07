<script lang="ts">
import type { PropType } from 'vue';

interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

export default {
  props: {
    todos: {
      type: Array as PropType<Todo[]>,
      required: true
    }
  },
  emits: ['deleteTodo']
};
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
          @click="$emit('deleteTodo', todo.id)"
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
