<template>
  <div class="game-board">
    <div class="box" v-for="n in 9" :key="n" />
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.game-board {
  background: grey;
  height: 500px;
  width: 500px;
  margin: auto;
  display: grid;
  gap: 5px;
  grid-template-columns: repeat(3, 1fr);
}

.box {
  padding: 10px;
  background-color: lightblue;
}
</style>
