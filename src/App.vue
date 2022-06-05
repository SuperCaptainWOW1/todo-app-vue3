<template>
  <img src="./assets/logo.png" alt="" />
  <h1>Vue 3 Todo app</h1>
  <form @submit.prevent="addNewTodo">
    <label for="">New Todo</label>
    <input type="text" name="newTodo" v-model="userInput" />
    <button>Add New Todo</button>
  </form>
  <button @click="toggleAllDone">Check all done</button>
  <button @click="removeAllTodos">Remove all</button>
  <ul>
    <li
      v-for="(todo, index) in todos"
      :key="todo.id"
      @click="toggleDone(todo)"
      class="todo"
    >
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(index)">X</button>
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";

export default {
  name: "App",
  setup() {
    const userInput = ref("");
    const todos = ref([]);

    const addNewTodo = () => {
      todos.value.push({
        id: Date.now(),
        text: userInput.value,
        done: false,
      });

      userInput.value = "";
    };

    const toggleDone = (todo) => {
      todo.done = !todo.done;
    };

    const removeTodo = (index) => {
      todos.value.splice(index, 1);
    };

    const toggleAllDone = () => {
      todos.value.forEach((todo) => (todo.done = true));
    };

    const removeAllTodos = () => {
      todos.value = [];
    };

    return {
      userInput,
      todos,
      addNewTodo,
      toggleDone,
      removeTodo,
      toggleAllDone,
      removeAllTodos,
    };
  },
};
</script>

<style>
body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
}
input,
textarea,
button,
p,
div,
section,
article,
select {
  display: "block";
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
}
.todo {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
</style>
