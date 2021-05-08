<template>
  <div
    :class="['cell', this.item === 0 ? 'cell_hidden' : '']"
    v-on:click="$emit('click-item', index)"
  >
    {{ item }}
  </div>
</template>

<script>
export default {
  name: "Cell",
  props: ["item", "index"],
};
</script>

<style scoped>
.cell {
  width: 90px;
  height: 90px;
  border: solid 2px gray;
  margin: 5px;
  text-align: center;
  font: bold 24px/90px Tahoma;
  border-radius: 10px;
  background-color: whitesmoke;
  padding: 0;
  box-sizing: border-box;
}
.cell_hidden {
  visibility: hidden;
}
</style>
