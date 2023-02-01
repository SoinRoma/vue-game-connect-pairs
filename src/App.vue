<template>
  <div class="app">
    <img class="logo" alt="Vue logo" src="./assets/logo.png" />
    <h1>Собери пару!</h1>
    <Board></Board>
  </div>
</template>

<script>
import Board from "@/components/Board.vue";

export default {
  name: "App",
  components: {
    Board,
  },
};
</script>

<style>
.app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.logo {
  width: 100px;
}
</style>
