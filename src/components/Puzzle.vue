<template>
  <transition-group name="cell-container" class="field" v-on:click="reset">
    <div v-for="(item, index) in items" :key="item">
      <Cell v-bind:item="item" v-bind:index="index" v-on:click-item="go" />
    </div>
  </transition-group>
</template>

<script>
import Cell from "./Cell";
import { eventBus } from "../main";

export default {
  name: "Puzzle",
  components: {
    Cell,
  },

  data() {
    return {
      items: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
        .sort(function () {
          return Math.random() - 0.5;
        })
        .concat(0),
      holeIndex: 15,
      move: {
        up: -4,
        right: 1,
        down: 4,
        left: -1,
      },
    };
  },
  created() {
    eventBus.$on("reset-game", this.reset);
  },
  methods: {
    // Функция перемещения ячеек
    swap: function (cell1, cell2) {
      const temp = this.items[cell1];
      this.$set(this.items, cell1, this.items[cell2]);
      this.$set(this.items, cell2, temp);
    },
    // Проверка возможности перемещения
    isMoveAvailable: function (i) {
      switch (this.holeIndex - i) {
        case this.move.up:
          return this.move.up;
        case this.move.right:
          return this.move.right;
        case this.move.down:
          return this.move.down;
        case this.move.left:
          return this.move.left;
        default:
          return false;
      }
    },
    // Клик по ячейке (перемещение)
    go: function (i) {
      if (this.isMoveAvailable(i)) {
        this.swap(i, this.holeIndex);
        this.holeIndex = i;
      }
    },
    // Перезапуск игры (не получился сам сброс, ивент отработал корректно)
    reset: function () {
      this.$forceUpdate();
    },
  },
};
</script>

<style scoped>
.field {
  display: flex;
  justify-content: center;
  align-content: center;
  flex-wrap: wrap;
  width: 400px;
  border: 1px solid black;
  border-radius: 5%;
}
.cell-container-move {
  transition: transform 0.3s;
}
</style>
