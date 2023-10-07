<script setup lang="ts">
import { ref, onBeforeMount } from 'vue';

import Panel from '@/components/Panel.vue';
import List from '@/components/List.vue';

interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

const status = ref<'loading' | 'finished' | 'error'>('loading');
const todos = ref<Todo[]>([]);

const addTodo = (todo: { title: string }) => {
  todos.value.push({ ...todo, id: todos.value.length + 1, completed: false });
};

const deleteTodo = (id: number) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};

onBeforeMount(async () => {
  try {
    status.value = 'loading';
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const todosJson = await response.json();

    todos.value = todosJson;
  } catch {
    status.value = 'error';
  } finally {
    status.value = 'finished';
  }
});
</script>

<template>
  <h1>Todo App 🔥</h1>
  <Panel @addTodo="addTodo" />
  <h2 v-if="status === 'loading'">Loading...</h2>
  <h2 v-if="status === 'error'">Error</h2>
  <List
    v-if="status !== 'loading' && !!todos.length"
    :todos="todos"
    @deleteTodo="deleteTodo"
  />
</template>

<style scoped>
.todoDone {
  text-decoration: line-through;
}
</style>
