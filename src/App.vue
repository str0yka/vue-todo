<script lang="ts">
import Panel from './components/Panel.vue';
import List from './components/List.vue';

interface Todo {
  id: number;
  title: string;
  description: string;
  checked: boolean;
}

export default {
  components: { Panel, List },
  data(): { todos: Todo[]; count: number; todo: Omit<Todo, 'id' | 'checked'> } {
    return {
      todos: [
        { id: 1, title: 'some title', description: 'some description', checked: false },
        { id: 2, title: 'some title', description: 'some description', checked: true },
        { id: 3, title: 'some title', description: 'some description', checked: false },
        { id: 4, title: 'some title', description: 'some description', checked: true },
        { id: 5, title: 'some title', description: 'some description', checked: false }
      ],
      count: 0,
      todo: { title: '', description: '' }
    };
  },

  methods: {
    addTodo(todo: { title: string; description: string }) {
      this.todos.push({ ...todo, id: this.todos.length + 1, checked: false });
      this.formReset();
    },
    deleteTodo(id: number) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    formReset() {
      this.todo.title = '';
      this.todo.description = '';
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
  <List
    :todos="todos"
    @deleteTodo="deleteTodo"
  />
</template>

<style scoped>
.todoDone {
  text-decoration: line-through;
}
</style>
