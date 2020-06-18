<template>
  <aside class="c-status">
    <button
      @click="openStatusList"
      class="status--button"
      :style="{ background: statusColor }"
      ref="statusLabel"
    >
      test{{ statusSelected }}
    </button>
    <transition name="fade">
      <form @keyup.enter="getStatus" class="status-list" v-if="showPicker">
        <fieldset>
          <legend class="sr-only">Change status</legend>
          <Item
            class="status-list--item"
            v-for="status in data"
            :status="status"
            :key="status.status_id + status.status_name"
            :style="{ background: status.color }"
            @updateLabel="updateLabel"
          />
        </fieldset>
      </form>
    </transition>
  </aside>
</template>

<script>
import Item from "../components/Item.vue";
export default {
  name: "StatusItem",
  components: { Item },
  data() {
    return {
      statusDefault: this.currentStatus,
      statusSelected: "",
      statusColor: null,
      selected: null,
      showPicker: false
    };
  },
  props: {
    currentStatus: String,
    data: Array
  },
  methods: {
    openStatusList() {
      this.showPicker = true;
    },
    getStatus() {
      this.$refs.statusLabel.style.setProperty("--label-background", "red");
      console.log(this.status, this.$refs.statusLabel);
    },
    updateLabel(label) {
      this.statusColor = label.color;
      this.statusSelected = label.name;
    }
  }
};
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
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

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
