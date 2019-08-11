<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todos">
      <TodoItem v-bind:todo="todo" v-on:delTodo="$emit('delTodo', todo.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
  name: "Todos",
  components: {
    TodoItem
  },
  props: {
    todos: Array
  }
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
</style>
