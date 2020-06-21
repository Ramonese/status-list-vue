<template>
  <div id="app">
    <h1>Projects and tasks</h1>
    <aside v-if="error" class="notification">
      <p>{{ error }}</p>
    </aside>
    <p v-if="isLoading">
      {{ loadingMessage }}
    </p>
    <transition name="fade">
      <section v-if="!isLoading">
        <ul class="task-list">
          <li
            class="task-list--item"
            v-for="item in taskItems"
            :key="item.name"
          >
            {{ item.name }}
            <StatusItem
              :data="statusDataTasks"
              :currentStatus="defaultTaskStatus"
            />
          </li>
        </ul>
        <ul class="task-list">
          <li
            class="task-list--item"
            v-for="item in projectItems"
            :key="item.name"
          >
            {{ item.name }}
            <StatusItem
              :data="statusDataProjects"
              :currentStatus="defaultProjectStatus"
            />
          </li>
        </ul>
      </section>
    </transition>
  </div>
</template>

<script>
import axios from "axios";
import StatusItem from "./components/StatusItem.vue";
//Cors server for development version of the app
const CORS_PROXY = "https://cors-anywhere.herokuapp.com/";
const apiUrl = "https://homeassignment.scoro.com/api/v2/statuses/list";
//Api request parameters to get task, project status
const params = {
  company_account_id: "apiplayground",
  apiKey: "ScoroAPI_8cacfb14f41d342",
  lang: "eng",
  filter: {
    module: ["projects", "tasks"]
  }
};
//data example test interface
const tasks = [{ name: "Task 1" }, { name: "Task 2" }];
const projects = [{ name: "Project 1" }, { name: "Project 2" }];
export default {
  name: "App",
  components: {
    StatusItem
  },
  data() {
    return {
      taskItems: tasks,
      projectItems: projects,
      statusDataTasks: null,
      statusDataProjects: null,
      defaultTaskStatus: null,
      defaultProjectStatus: null,
      error: null,
      isLoading: true,
      loadingMessage: "Fetching your data"
    };
  },
  created() {
    axios
      .post(CORS_PROXY + apiUrl, params)
      .then(response => {
        const data = response.data.data;
        this.statusDataTasks = data.filter(item => item.module == "tasks");
        this.statusDataProjects = data.filter(
          item => item.module == "projects"
        );
        //Example test interface to set default status for task, project
        this.defaultTaskStatus = this.statusDataTasks.filter(
          item => item.is_default == 1
        );
        this.defaultProjectStatus = this.statusDataProjects.filter(
          item => item.is_default == 1
        );
        if (this.statusDataTasks && this.statusDataProjects) {
          this.isLoading = false;
        }
      })
      .catch(error => {
        this.error = "Please, try again " + error;
      });
  }
};
</script>

<style>
:root {
  --white: #fff;
  --text-color: #1f2226;
  --text-active: #043159;
  --label-background: #47c1bf;
  --hover-color: #f7f9fd;
  --focus-color: #ebf5fa;
  --focus-border: transparent;
  --border-radius: 4px;
}
@font-face {
  font-family: "Inter";
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url("./assets/font/Inter-Medium.woff") format("woff");
}
#app {
  font-family: Inter, Helvetica, Arial, sans-serif;
  color: var(--text-color);
  font-size: 12px;
  line-height: 16px;
  max-width: 100em;
  margin: 5em auto;
  padding: 3em;
}
/*Example interface style, not realted to test*/
h1 {
  font-weight: normal;
  margin-bottom: 2em;
}
.task-list {
  list-style: none;
  display: grid;
  width: max-content;
  grid-template-columns: 1fr;
  grid-gap: 2em;
  margin-bottom: 3em;
}
.task-list--item {
  display: grid;
  grid-template-columns: max-content 1fr;
  grid-gap: 3em 10px;
  align-items: center;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease-in;
  opacity: 1;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
