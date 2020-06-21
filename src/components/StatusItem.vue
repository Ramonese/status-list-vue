<template>
  <aside class="c-status">
    <button
      class="status--button"
      :style="{ background: statusColor }"
      @click.stop="openStatusList"
    >
      {{ statusName }}
    </button>
    <div v-show="showPicker">
      <form class="status-list" v-click-outside="onClickOutside">
        <fieldset>
          <legend class="sr-only">Change status</legend>
          <div
            v-for="status in data"
            :key="status.status_id + status.status_name"
          >
            <StatusName
              class="status-list--item"
              :status="status"
              :activeStatusClass="statusName"
              @updateLabel="updateLabel"
            />
          </div>
        </fieldset>
      </form>
    </div>
  </aside>
</template>

<script>
import vClickOutside from "v-click-outside";
import StatusName from "../components/StatusName.vue";
export default {
  name: "StatusItem",
  components: { StatusName },
  props: {
    currentStatus: Array,
    data: Array
  },
  data() {
    return {
      statusName: this.currentStatus[0].status_name,
      statusColor: this.currentStatus[0].color,
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
    onClickOutside() {
      this.showPicker = false;
    },
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
  padding: 8px 0;
}
.status-list--item {
  padding: 10px 16px;
  display: flex;
  align-items: center;
  cursor: pointer;
}
.status-list--item:hover {
  background-color: var(--hover-color);
}
.status-list--item.active {
  color: var(--text-active);
  background-color: var(--focus-color);
  border-left: 2px solid var(--accent);
  font-weight: 600;
}
.status-list--item.active .status-color {
  --focus-border: var(--white);
}
.status--button {
  -webkit-appearance: button;
  font-family: inherit;
  font-weight: normal;
  font-size: inherit;
  position: relative;
  padding: 2px 8px;
  cursor: pointer;
  color: var(--white);
  background: var(--label-background);
  border: 0;
  border-radius: var(--border-radius);
}
.status--button:focus {
  outline-color: lightgrey;
}
</style>
