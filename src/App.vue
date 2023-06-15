<template>
  <main class="app">
    <section class="greeting">
      <h2 class="title">
        What's up
        <input type="text" placeholder="name here" v-model="name" />
      </h2>
    </section>
    <section class="createToDo">
      <h3>Create a To Do</h3>
      <form @submit.prevent="addTodo">
        <h4>What's on your to-do list</h4>
        <input
         type="text" 
         placeholder="e.g make a video" 
         v-model="input_content" />
        <h4>Pick a categorie</h4>
        <div class="options">
        <input type="radio" name="category" value="Business" v-mode="input_category">
        </div>
      </form>
    </section>
  </main>
</template>

<script>
import { onMounted, ref, computed, watch } from 'vue';

export default {
  name: 'App',
  setup() {
    const name = ref('');
    const todos = ref([]);
    const input_content = ref('');
   const input_category = ref(null);
    const addTodo = () => {
      // Add logic for adding a todo
    };

    const sortedTodos = computed(() => todos.value.sort((a, b) => b.createAt - a.createAt));

    watch(name, (newVal) => {
      localStorage.setItem('name', newVal);
    });

    onMounted(() => {
      name.value = localStorage.getItem('name');
    });

    return {
      name,
      todos,
      input_content,
      input_category,
      addTodo,
      todos_asc: sortedTodos,
    };
  },
};
</script>

<style></style>
