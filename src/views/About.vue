<template>
  <div id="app" >
    <h1 class="header">Todo App + Composition API</h1>
    <div id="nav" class="header">
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
    </div>
    <form @submit.prevent="addNewTodo">
      <label>New Todo</label>
      <input v-model="newTodo" type="text" name="newTodo">
      <button>Add new list</button>
    </form> 
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">{{todo.content}}</h3>
      </li>
    </ul>
    
  </div>
  
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    return {
      todos,
      newTodo,
      addNewTodo,
    }
  }
}
</script>

<style scoped>
  body{
    font-family: sans-serif;
    padding-bottom: 1em;
    padding-top: 1em;
    font-size: 2em;
    width: 80%;
    margin: 0 auto;
  }
  input, textarea, button, p, div, section, article, select {
    display: 'block';
    width: 100%;
    font-family: sans-serif;
    margin: 0.5em;
    font-size: 1em;
  }
  .done {
    text-decoration: line-through;
  }

</style>