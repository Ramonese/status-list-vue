<template>
  <div id="app">
    <StatusItem currentStatus="test" />
  </div>
</template>

<script>
import axios from "axios";
import StatusItem from "./components/StatusItem.vue";
// Make a request for a user with a given ID
const CORS_PROXY = "https://cors-anywhere.herokuapp.com/";
const params = {
  company_account_id: "apiplayground",
  apiKey: "ScoroAPI_8cacfb14f41d342",
  lang: "eng",
  filter: {
    module: ["projects", "tasks"]
  }
};
axios
  .post(
    CORS_PROXY + "https://homeassignment.scoro.com/api/v2/statuses/list",
    params
  )
  .then(function(response) {
    // handle success
    console.log(response.data);
  })
  .catch(function(error) {
    // handle error
    console.log(error);
  })
  .then(function() {
    // always executed
  });
export default {
  name: "App",
  components: {
    StatusItem
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
  text-align: center;
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
</style>
