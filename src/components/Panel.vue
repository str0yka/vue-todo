<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits<{ addTodo: [{ title: string }] }>();

const todo = ref({ title: '' });

const formReset = () => {
  todo.value.title = '';
};

const onSubmit = () => {
  emit('addTodo', todo.value);
  formReset();
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
