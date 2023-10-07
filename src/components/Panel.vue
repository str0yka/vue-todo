<script lang="ts">
interface Todo {
  id: number;
  title: string;
  description: string;
  checked: boolean;
}

export default {
  emits: ['addTodo'],
  data(): { todo: Omit<Todo, 'id' | 'checked'> } {
    return {
      todo: { title: '', description: '' }
    };
  },

  methods: {
    onSubmit() {
      this.$emit('addTodo', this.todo);
      this.formReset();
    },
    formReset() {
      this.todo.title = '';
      this.todo.description = '';
    }
  }
};
</script>

<template>
  <form @submit.prevent="onSubmit">
    <input
      type="text"
      placeholder="title"
      v-model="todo.title"
    />
    <input
      type="text"
      placeholder="description"
      v-model="todo.description"
    />
    <button type="submit">add todo</button>
  </form>
</template>
