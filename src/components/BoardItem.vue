<template>
  <div class="board-item">{{ cell ? cell : "" }}</div>
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
  },
};
</script>

<style scoped>
.board-item {
  border: 1px solid #2c3e50;
  width: 48px;
  height: 48px;
}
</style>
