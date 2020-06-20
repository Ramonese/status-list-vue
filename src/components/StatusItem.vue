<template>
  <aside class="c-status">
    <button
      class="status--button"
      :style="{ background: statusColor }"
      @click.stop="openStatusList"
      ref="statusLabel"
    >
      {{ statusName }}
    </button>
    <transition name="fade">
      <div v-if="showPicker">
        <form class="status-list" v-click-outside="onClickOutside">
          <fieldset>
            <legend class="sr-only">Change status</legend>
            <div
              v-for="status in data"
              :key="status.status_id + status.status_name"
            >
              <template v-if="status.module == module">
                <Item
                  class="status-list--item"
                  :status="status"
                  @updateLabel="updateLabel"
                />
              </template>
            </div>
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
      statusName: this.currentStatus,
      statusColor: null,
      selected: null,
      showPicker: false
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
      this.statusName = label.name;
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
  margin: 0;
  padding: 0;
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
  -webkit-appearance: button;
  position: relative;
  padding: 2px 8px;
  cursor: pointer;
  color: var(--white);
  background: var(--label-background);
  border: 0;
  border-radius: var(--border-radius);
}
.status-label {
  display: inline-block;
  padding-left: 8px;
  line-height: 1;
  white-space: nowrap;
}
.status-list--item {
  padding: 10px 16px;
  display: flex;
  align-items: center;
}
.status-list--item:hover {
  background-color: var(--hover-color);
}
.status-list--item:active {
  color: var(--text-active);
  background-color: var(--focus-color);
}
.status-list--item:active .status-color {
  --focus-border: white;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
