<script lang="ts">
import { onMounted } from 'vue';

export default {
  props: ['todos'],
  emits: ['deleteTodo']
};
</script>

<template>
  <h2 v-if="!todos.length">no todos</h2>
  <ul
    v-if="!!todos.length"
    v-for="todo in todos"
    :key="todo.id"
  >
    <li>
      <div>
        <h2 :class="{ todoDone: todo.checked }">{{ todo.title }}</h2>
        <p>{{ todo.description }}</p>
        <input
          type="checkbox"
          v-model="todo.checked"
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
