<template>
  <div id="app">
    <aside v-if="error" class="notification">
      <p>{{ error }}</p>
    </aside>
    <p v-if="isLoading">
      {{ loadingMessage }}
    </p>
    <section v-else>
      <ul class="task-list">
        <li class="task-list--item" v-for="item in taskItems" :key="item.name">
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
    <!-- <div v-for="status in statusData" :key="status.status_id">
      <input
        type="radio"
        name="status"
        :value="status.status_name"
        :id="status.status_id"
        :color="status.color"
        @change="changeStatus"
      />
      <label :for="status.status_id" class="status-label">{{
        status.status_name
      }}</label>
    </div> -->
    <p>status {{ defaultTaskStatus }}, {{ defaultProjectStatus }}</p>
    {{ statusDataTasks }}<br />
    {{ statusDataProjects }}
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
        console.log(this.statusDataTasks.length);
        console.log(this.statusDataProjects.length);
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
/* @font-face {
  font-family: "Inter";
  font-style: normal;
  font-weight: 600;
  font-display: swap;
  src: url("Inter-SemiBold.woff2?v=3.12") format("woff2"),
    url("Inter-SemiBold.woff?v=3.12") format("woff");
} */
#app {
  font-family: Inter, Helvetica, Arial, sans-serif;
  color: var(--text-color);
  font-size: 12px;
  line-height: 16px;
  max-width: 100em;
  margin: 5em auto;
}

.task-list {
  list-style: none;
  display: grid;
  width: max-content;
  grid-template-columns: 1fr;
  grid-gap: 2em;
}
.task-list--item {
  display: grid;
  grid-template-columns: max-content 1fr;
  grid-gap: 3em 10px;
  align-items: center;
}
</style>
