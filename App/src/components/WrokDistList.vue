<template>
  <div>
    <todo v-bind:key="todo" v-on:delete-todo="deleteTodo" v-for="todo in todos" :todo.sync="todo"></todo>
  </div>
</template>

<script type = "text/javascript" >
import Todo from "./WorkDist";
import axios from "axios";
//const baseURL = "http://localhost:3000/todos/";

export default {
  props: ["todos"],
  components: {
    Todo
  },
  methods: {
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      axios.delete("http://localhost:3000/todos/" + this.todos[todoIndex].id);
      this.todos.splice(todoIndex, 1);
    }
  }
};
</script>