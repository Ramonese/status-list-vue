<template>
  <aside class="status">
    <button @click="openStatusList" class="status--button">{{ status }}</button>
    <form @submit="getStatus" class="status-list">
      <fieldset>
        <legend class="sr-only">Change status</legend>
        <div class="status-list--item">
          <input
            type="radio"
            value="waiting"
            id="1"
            v-model="status"
            name="status"
          />
          <label for="1">Waiting</label>
        </div>
        <div class="status-list--item">
          <input
            type="radio"
            id="2"
            name="status"
            value="test"
            v-model="status"
          />
          <label for="2">Test</label>
        </div>
        <div class="status-list--item">
          <input
            type="radio"
            id="3"
            name="status"
            v-model="status"
            value="ready"
          />
          <label for="3">Ready</label>
        </div>
      </fieldset>
    </form>
    <!-- <div>
      <input
        type="radio"
        value="One"
        :checked="picked == 'One'"
        @change="e => (picked = e.target.value)"
      />
      <input
        type="radio"
        value="Two"
        :checked="picked == 'Two'"
        @change="e => (picked = e.target.value)"
      />
      <span>Picked: {{ picked }}</span>
    </div> -->
  </aside>
</template>

<script>
export default {
  name: "StatusItem",
  data() {
    return {
      status: this.currentStatus
      //picked: ""
    };
  },
  props: {
    currentStatus: String
  },
  methods: {
    openStatusList() {},
    getStatus() {
      console.log(this.status);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
