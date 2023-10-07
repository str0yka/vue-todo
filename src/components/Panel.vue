<script lang="ts">
interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

export default {
  emits: ['addTodo'],
  data(): { todo: { title: string } } {
    return {
      todo: { title: '' }
    };
  },

  methods: {
    onSubmit() {
      this.$emit('addTodo', this.todo);
      this.formReset();
    },
    formReset() {
      this.todo.title = '';
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
    <button type="submit">add todo</button>
  </form>
</template>
