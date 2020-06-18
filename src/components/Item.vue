<template>
  <div>
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
  </div>
</template>

<script>
export default {
  name: "Item",
  // data() {
  //   return {
  //     statusDefault: this.currentStatus,
  //     statusSelected: "",
  //     statusColor: null,
  //     selected: null
  //   };
  // },
  props: {
    status: Object
  },
  methods: {
    openStatusList() {
      alert("click");
    },
    getStatus() {
      this.$refs.statusLabel.style.setProperty("--label-background", "red");
      console.log(this.status, this.$refs.statusLabel);
    },
    changeStatus($event) {
      const label = {
        name: $event.target.value,
        color: this.status.color
      };
      console.log("click status", label);
      this.$emit("updateLabel", label);
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
