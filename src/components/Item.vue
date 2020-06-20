<template>
  <div>
    <!-- <input
      type="radio"
      name="status"
      :value="status.status_name"
      :id="status.status_id + status.status_name"
      :style="{ color: status.color }"
      @change="changeStatus"
    /> -->
    <span class="status-color" :style="{ background: status.color }"></span>
    <label
      :for="status.status_id"
      class="status-label"
      @click="changeStatus"
      @up="changeStatus"
      >{{ status.status_name }}</label
    >
  </div>
</template>

<script>
export default {
  name: "Item",
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
    changeStatus() {
      const label = {
        name: this.status.status_name,
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
[type="radio"] {
  position: absolute;
  left: -9999px;
}
[type="radio"]:checked + label,
[type="radio"]:not(:checked) + label {
  position: relative;
  padding-left: 28px;
  cursor: pointer;
  line-height: 20px;
  display: inline-block;
  color: #666;
}
[type="radio"]:checked + label:before,
[type="radio"]:not(:checked) + label:before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 18px;
  height: 18px;
  border: 1px solid #ddd;
  border-radius: 100%;
  background: currentColor;
}
.status-color {
  --focus-border: transparent;
  display: inline-block;
  height: 12px;
  width: 12px;
  border-radius: 50%;
  border: 2px solid var(--focus-border);
}
</style>
