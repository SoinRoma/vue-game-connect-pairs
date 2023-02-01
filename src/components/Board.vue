<template>
  <div>Уровень: {{ level }}</div>
  <div v-if="gameStatus === 1" class="win">Вы выиграли!!!</div>
  <div
    class="board"
    :style="{ width: 50 * size + 'px', height: 50 * size + 'px' }"
  >
    <BoardItem
      v-for="(cell, index) in cells"
      :cell="cell"
      :key="cell + '-' + index"
      @mousedown="mousedown(index)"
      @mouseup="mouseup(index)"
      @mousemove="go(index)"
      :selected="checkRoad(index)"
      :closed="checkClosedRoad(index)"
    ></BoardItem>
  </div>
  <div @click="reload()" class="reload">Сбросить уровень</div>
</template>

<script>
import { ref } from "vue";
import BoardItem from "./BoardItem.vue";
export default {
  name: "board-main",
  components: {
    BoardItem,
  },
  setup() {
    let cells = ref([3, 1, 0, 1, 0, 0, 0, 0, 2, 0, 0, 0, 2, 0, 0, 3]);
    const path = ref([]);
    let size = ref(4);
    let closedPath = ref([]);
    let level = ref(1);
    const maxLevel = 2;
    let gameStatus = ref(0);

    const mousedown = (index) => {
      path.value = [];
      if (cells.value[index] && !checkClosedRoad(index)) {
        path.value.push(index);
      }
    };

    const mouseup = (index) => {
      if (
        index !== path.value[0] &&
        cells.value[index] === cells.value[path.value[0]]
      ) {
        closedPath.value = [...closedPath.value, ...path.value];
      }

      path.value = [];
      checkLevel();
    };

    const checkLevel = () => {
      let completed = true;

      cells.value.forEach((cell, index) => {
        if (cell && !checkClosedRoad(index)) {
          completed = false;
        }
      });

      if (completed) {
        goToNextLevel();
      }
    };

    const goToNextLevel = () => {
      level.value += 1;
      gameStatus.value = 0;
      if (level.value > maxLevel) {
        level.value = 1;
        gameStatus.value = 1;
      }
      start(level.value);
    };

    const checkRoad = (index) => {
      return path.value.findIndex((p) => p === index) > -1;
    };

    const checkClosedRoad = (index) => {
      return closedPath.value.findIndex((p) => p === index) > -1;
    };

    const start = (level) => {
      if (level === 1) {
        cells.value = [3, 1, 0, 1, 0, 0, 0, 0, 2, 0, 0, 0, 2, 0, 0, 3];
        size.value = 4;
      }

      if (level === 2) {
        cells.value = [
          0, 2, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 2, 0, 0, 3, 0, 0, 0, 0, 0, 0, 3,
          0, 0,
        ];
        size.value = 5;
      }

      path.value = [];
      closedPath.value = [];
    };

    start(level.value);

    const reload = () => {
      start(level.value);
    };

    const go = (index) => {
      if (path.value.length) {
        const lastIndex = path.value[path.value.length - 1];

        if (
          (Math.abs(lastIndex - index) === 1 ||
            Math.abs(lastIndex - index) === size.value) &&
          !checkClosedRoad(index)
        ) {
          path.value.push(index);
        }

        if (
          checkClosedRoad(index) ||
          (cells.value[index] &&
            cells.value[index] !== cells.value[path.value[0]])
        ) {
          path.value = [];
        }
      }
    };
    return {
      cells,
      level,
      size,
      gameStatus,
      mousedown,
      mouseup,
      checkRoad,
      checkClosedRoad,
      go,
      reload,
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
  margin: 20px auto;
}

.reload {
  text-decoration: underline;
  cursor: pointer;
}

.win {
  font-weight: 700;
}
</style>
