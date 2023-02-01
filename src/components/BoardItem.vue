<template>
  <div
    :class="
      'board-item ' + (selected ? 'selected' : '') + (closed ? 'closed' : '')
    "
  >
    <i v-if="cell" :class="'icon icon-' + cell"></i>
  </div>
</template>

<script>
export default {
  name: "board-item",
  props: {
    cell: {
      type: Number,
      required: false,
      default: 0,
    },
    selected: {
      type: Boolean,
      required: false,
      default: false,
    },
    closed: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
};
</script>

<style scoped>
.board-item {
  border: 1px solid #2c3e50;
  width: 48px;
  height: 48px;
  position: relative;
}

.selected {
  background-color: rgba(45, 191, 70, 0.727);
}
.closed {
  background-color: rgba(45, 191, 69, 0.353);
}

.icon {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}

.icon-1,
.icon-2,
.icon-3 {
  background: url("../assets/icons.png");
  background-size: 150px 150px;
}

.icon-1 {
  background-position: 0 0;
}

.icon-2 {
  background-position: 50px 0;
}

.icon-3 {
  background-position: 100px 0;
}
</style>
