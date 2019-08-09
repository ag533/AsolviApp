<template>
  <div id="app">
      <workDist-list v-bind:todos="todos"></workDist-list>
      <create-todo v-on:add-todo="addTodo" @update="addTodo"></create-todo>
  </div>
</template>

<script>
import WorkDistList from "./components/WrokDistList";
import CreateTodo from "./components/CreateWorkDist";
import axios from "axios";
const baseURL = "http://localhost:3000/todos";

export default {
  name: "app",
  components: {
    WorkDistList,
    CreateTodo
  },

  data() {
    return {
      todos: [],
      todoName: ""
    };
  },

  async created() {
    try {
      const res = await axios.get(baseURL);

      this.todos = res.data;
    } catch (e) {
      alert(e);
    }
  },

  methods: {
    addTodo(data) {
      const len = this.todos.length;
      const title = data.title;
      const project = data.project;
      const done = data.done;
      this.todos.push({
        id: len + 1,
        title: title,
        project: project,
        done: done
      });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
