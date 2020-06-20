<template>
  <aside class="c-status">
    <button
      class="status--button"
      :style="{ background: statusColor }"
      @click.stop="openStatusList"
      ref="statusLabel"
    >
      {{ currentStatus }}
    </button>
    <transition name="fade">
      <div v-if="showPicker">
        <form class="status-list" v-click-outside="onClickOutside">
          <fieldset>
            <legend class="sr-only">Change status</legend>
            <Item
              class="status-list--item"
              v-for="status in data"
              :status="status"
              :moduleName="status.module"
              :key="status.status_id + status.status_name"
              @updateLabel="updateLabel"
            />
          </fieldset>
        </form>
      </div>
    </transition>
  </aside>
</template>

<script>
import vClickOutside from "v-click-outside";
import Item from "../components/Item.vue";
export default {
  name: "StatusItem",
  components: { Item },
  props: {
    currentStatus: String,
    data: Array,
    module: String
  },
  data() {
    return {
      statusDefault: this.currentStatus,
      statusSelected: "",
      statusColor: null,
      selected: null,
      showPicker: true
    };
  },
  directives: {
    clickOutside: vClickOutside.directive
  },

  methods: {
    openStatusList() {
      this.showPicker = true;
    },
    onClickOutside(event) {
      console.log("Clicked outside. Event: ", event);
      console.log("Element clicked on:", event.target);
      this.showPicker = false;
    },
    // getStatus() {
    //   this.$refs.statusLabel.style.setProperty("--label-background", "red");
    //   console.log(this.status, this.$refs.statusLabel);
    // },
    updateLabel(label) {
      this.statusColor = label.color;
      this.currentStatus = label.name;
      this.showPicker = false;
    }
  }
};
</script>

<style>
ul {
  list-style-type: none;
  padding: 0;
}

fieldset {
  border: none;
}
.c-status {
  position: relative;
  max-width: max-content;
  display: flex;
  flex: 1 1 auto;
  flex-direction: column;
  align-items: baseline;
}
.status-list {
  position: absolute;

  background: var(--white);
  border-radius: var(--border-radius);
  box-shadow: 0px 8px 32px rgba(31, 34, 38, 0.12),
    0px 2px 6px rgba(31, 34, 38, 0.08);
  z-index: 1;
}
.status--button {
  position: relative;
  padding: 2px 8px;
  -webkit-appearance: button;
  border: 0;
  border-radius: var(--border-radius);
  cursor: pointer;
  color: var(--white);
  background: var(--label-background);
}

.status-label {
  display: inline-block;
  padding: 8px;
  white-space: nowrap;
}
.status-list--item {
  padding: 0 16px;
}
.status-list--item:hover {
  background-color: var(--hover-color);
}
.status-list--item:active {
  background-color: var(--focus-color);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
