<template>
  <div id="app">
    <aside v-if="error" class="notification">
      <p>{{ error }}</p>
    </aside>
    <section>
      <ul class="task-list">
        <li class="task-list--item">
          Task 1 name
          <StatusItem currentStatus="Completed" :data="statusData" />
        </li>
        <li class="task-list--item">
          <p>Task 2 name Task 2 name</p>
          <StatusItem currentStatus="Completed" :data="statusData" />
        </li>
        <li class="task-list--item">
          <p>Project 3 name</p>
          <StatusItem currentStatus="Completed" :data="statusData" />
        </li>
      </ul>
    </section>

    {{ statusData }}
  </div>
</template>

<script>
import axios from "axios";
import StatusItem from "./components/StatusItem.vue";
//Cors server for development version of the app
const CORS_PROXY = "https://cors-anywhere.herokuapp.com/";
const apiUrl = "https://homeassignment.scoro.com/api/v2/statuses/list";
const params = {
  company_account_id: "apiplayground",
  apiKey: "ScoroAPI_8cacfb14f41d342",
  lang: "eng",
  filter: {
    module: ["projects", "tasks"]
  }
};

export default {
  name: "App",
  components: {
    StatusItem
  },
  data() {
    return {
      statusData: null,
      error: null
    };
  },
  created() {
    axios
      .post(CORS_PROXY + apiUrl, params)
      .then(response => (this.statusData = response.data.data))
      .catch(error => {
        this.error = "Please, try again " + error;
        console.log(error);
      })
      .then(function() {
        // always executed
      });
  }
};
</script>

<style>
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
  color: #2c3e50;
  font-size: 12px;
  line-height: 16px;
}
:root {
  --white: #fff;
  --blue: #47c1bf;
  --label-background: #47c1bf;
  --hover-color: #f7f9fd;
  --focus-color: red;
}
.task-list {
  list-style: none;
  display: grid;
  width: max-content;
  grid-template-columns: 1fr;
}
.task-list--item {
  display: grid;
  grid-template-columns: max-content 1fr;
  grid-gap: 3em 10px;
}
</style>
