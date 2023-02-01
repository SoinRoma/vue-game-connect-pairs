<template>
  <div class="board">
    <BoardItem
      v-for="cell in cells"
      :cell="cell"
      :key="'cell-' + cell"
    ></BoardItem>
  </div>
</template>

<script>
import BoardItem from "./BoardItem.vue";
export default {
  name: "board-main",
  components: {
    BoardItem,
  },
  data() {
    return {
      cells: [3, 1, 0, 1, 0, 0, 0, 0, 2, 0, 0, 0, 2, 0, 0, 3],
    };
  },
};
</script>

<style scoped>
.board {
  width: 200px;
  height: 200px;
  display: flex;
  flex-wrap: wrap;
  margin: 0 auto;
}
</style>
