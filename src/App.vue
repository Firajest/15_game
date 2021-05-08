<template>
  <div id="app">
    <div class="timer">
      <Timer />
    </div>
    <div class="game">
      <Puzzle />
    </div>
  </div>
</template>

<script>
import Puzzle from "./components/Puzzle.vue";
import Timer from "./components/Timer.vue";

export default {
  name: "App",
  components: {
    Puzzle,
    Timer,
  },
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
}
.game {
  display: flex;
  justify-content: center;
  margin: 55px 0 0;
}
</style>
