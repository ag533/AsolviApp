 <template>
  <div class="ui basic content center aligned segment">
    <button class="ui basic button icon" v-on:click="openForm" v-show="!isCreating">
      <i class="plus icon"></i>
    </button>
    <div class="ui centered card" v-show="isCreating">
      <div class="content">
        <div class="ui form">
          <div class="field">
            <label>Title</label>
            <input v-model="titleText" type="text" ref="title" defaultValue />
          </div>
          <div class="field">
            <label>Project</label>
            <input v-model="projectText" type="text" ref="project" defaultValue />
          </div>
          <div class="ui two button attached buttons">
            <button class="ui basic blue button" v-on:click="sendForm()">Create</button>
            <button class="ui basic red button" v-on:click="closeForm">Cancel</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
let baseURL = "http://localhost:3000/todos/";
export default {
  data() {
    return {
      titleText: "",
      projectText: "",
      isCreating: false
    };
  },
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    sendForm() {
      if (this.titleText != null && this.projectText != null) {
        const title = this.titleText;
        const project = this.projectText;
        axios.post(baseURL, {
          title: this.titleText,
          project: this.projectText
        });
        this.$emit("update", {
          title: title,
          project: project
        });
        this.newTodoText = "";
      }
      this.isCreating = false;
    }
  }
};
</script>