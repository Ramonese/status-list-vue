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
</style>
