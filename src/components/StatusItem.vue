<template>
  <aside class="c-status">
    <button @click="openStatusList" class="status--button" ref="statusLabel">
      {{ status }}
    </button>
    <form @keyup.enter="getStatus" class="status-list">
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
          <label for="1" class="status-label">Waiting</label>
        </div>
        <div class="status-list--item">
          <input
            type="radio"
            id="2"
            name="status"
            value="test"
            v-model="status"
          />
          <label for="2" class="status-label">Test</label>
        </div>
        <div class="status-list--item">
          <input
            type="radio"
            id="3"
            name="status"
            v-model="status"
            value="ready"
          />
          <label for="3" class="status-label">Ready</label>
        </div>
      </fieldset>
    </form>
  </aside>
</template>

<script>
export default {
  name: "StatusItem",
  data() {
    return {
      status: this.currentStatus,
      //picked: ""
    };
  },
  props: {
    currentStatus: String,
  },
  methods: {
    openStatusList() {
      alert("click");
    },
    getStatus() {
      this.$refs.statusLabel.style.setProperty("--label-background", "red");
      console.log(this.status, this.$refs.statusLabel);
    },
  },
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
fieldset {
  border: none;
}
.c-status {
  max-width: max-content;
  display: flex;
  flex: 1 1 auto;
  flex-direction: column;
  align-items: baseline;
}
.status-list {
  padding: 16px;
  background: var(--white);
  box-shadow: 0px 8px 32px rgba(31, 34, 38, 0.12),
    0px 2px 6px rgba(31, 34, 38, 0.08);
}
.status--button {
  padding: 2px 8px;
  -webkit-appearance: button;
  border: 0;
  border-radius: 4px;
  cursor: pointer;
  color: var(--white);
  background: var(--label-background);
}
.status--button:focus {
  outline: 2px solid black;
}
.status-label {
  display: inline-block;
  padding: 8px;
}
.status-list--item:hover {
  background-color: var(--hover-color);
}
.status-list--item:active {
  background-color: var(--focus-color);
}
</style>
