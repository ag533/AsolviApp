<template>
  <div class="ui centered card" style="display:inline-block; border:solid 3px #ccc">
    <!-- // Todo shown when we are not in editing mode. -->
    <div class="content" v-show="!isEditing">
      <div class="header">{{ todo.title }}</div>
      <div class="meta">{{ todo.project }}</div>
      <div class="extra content">
        <span class="right floated edit icon" v-on:click="showForm">
          <i class="edit icon"></i>
        </span>
        <span class="right floated trash icon" v-on:click="deleteTodo(todo)">
          <i class="trash icon"></i>
        </span>
      </div>
    </div>
    <!-- // form is visible when we are in editing mode -->
    <div class="content" v-show="isEditing">
      <div class="ui form">
        <div class="field">
          <label>Title</label>
          <input type="text" v-model="todo.title" />
        </div>
        <div class="field">
          <label>Project</label>
          <input type="text" v-model="todo.project" />
        </div>
        <div class="ui two button attached buttons">
          <button class="ui basic blue button" v-on:click="saveForm">Save</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["todo"],
  data() {
    return {
      isEditing: false
    };
  },
  methods: {
    deleteTodo(todo) {
      this.$emit("delete-todo", todo);
    },
    showForm() {
      this.isEditing = true;
    },
    saveForm() {
      this.isEditing = false;
      axios.put("http://localhost:3000/todos/" + this.todo.id + "/", {
        title: this.todo.title,
        project: this.todo.project
      });
    },
    hideForm() {
      this.isEditing = false;
    }
  }
};
</script>
<style>
</style>