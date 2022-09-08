<script setup lang="ts">

import { ref, reactive} from "vue";
import TodoComponent from './TodoComponent.vue'

const inputValue = ref('')
let todos = reactive({todosProp: ['hiuhsf']})

function createTodo() {
  todos.todosProp.push(inputValue.value);
  inputValue.value = '';
}

function removeTodo(todo: string) {
  todos.todosProp = todos.todosProp.filter( (t) => t !== todo);
}

</script>

<template>
<div class="container">
  <h1>My todos</h1>
  <input v-model="inputValue" @keyup.enter="createTodo"/>

  <ul v-if="todos.todosProp.length">
    <li v-for="todo in todos.todosProp" :key="todo">
      <TodoComponent :todo="todo" @remove-me="removeTodo(todo)"> - </TodoComponent>
    </li>
  </ul>
</div>

</template>

<style>
.container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-start;
}
</style>