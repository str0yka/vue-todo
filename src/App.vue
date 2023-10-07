<script lang="ts">
import Panel from './components/Panel.vue';
import List from './components/List.vue';

interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

export default {
  components: { Panel, List },
  data(): { status: 'loading' | 'finished' | 'error'; todos: Todo[]; todo: { title: string } } {
    return {
      status: 'loading',
      todos: [],
      todo: { title: '' }
    };
  },

  async beforeMount() {
    try {
      this.status = 'loading';
      const response = await fetch('https://jsonplaceholder.typicode.com/todos');
      const todos = await response.json();

      this.todos = todos;
    } catch {
      this.status = 'error';
    } finally {
      this.status = 'finished';
    }
  },

  methods: {
    addTodo(todo: { title: string; description: string }) {
      this.todos.push({ ...todo, id: this.todos.length + 1, completed: false });
    },
    deleteTodo(id: number) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    }
  },

  updated() {
    console.log(this.todos);
  }
};
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
