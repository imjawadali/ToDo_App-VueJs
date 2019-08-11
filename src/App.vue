<template>
  <div id="app">
    <Header />
    <AddTodo v-on:addTodo="addTodo" />
    <Todos v-bind:todos="todos" v-on:delTodo="deleteTodo" />
  </div>
</template>

<script>
import Axios from "axios";

import Header from "./components/Layout/Header";
import AddTodo from "./components/AddTodo";
import Todos from "./components/Todos";

export default {
  name: "app",
  components: {
    Header,
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    /* eslint-disable */
    deleteTodo(id) {
      Axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(() => (this.todos = this.todos.filter(todo => todo.id !== id)))
        .catch(error => console.log(error));
    },
    addTodo(newTodo) {
      Axios.post("https://jsonplaceholder.typicode.com/todos", newTodo)
        .then(res => (this.todos = [...this.todos, res.data]))
        .catch(error => console.log(error));
    }
  },
  created() {
    Axios.get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(res => (this.todos = res.data))
      .catch(error => console.log(error));
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
