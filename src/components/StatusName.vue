<template>
  <div
    :class="{ active: status.status_name === activeStatusClass }"
    @click="changeStatus"
  >
    <span class="status-color" :style="{ background: status.color }"></span>
    <label class="status-label">{{ status.status_name }}</label>
  </div>
</template>

<script>
export default {
  name: "StatusName",
  props: {
    status: Object,
    activeStatusClass: String
  },
  methods: {
    changeStatus() {
      const label = {
        name: this.status.status_name,
        color: this.status.color
      };
      this.$emit("updateLabel", label);
    }
  }
};
</script>

<style>
.status-color {
  --focus-border: transparent;
  display: inline-block;
  height: 12px;
  width: 12px;
  border-radius: 50%;
  border: 2px solid var(--focus-border);
}
.status-label {
  cursor: inherit;
  display: inline-block;
  padding-left: 8px;
  line-height: 1;
  white-space: nowrap;
}
</style>
