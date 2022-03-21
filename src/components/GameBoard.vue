<template>
  <div>
    <h1>Player {{ player }} turn</h1>
    <h1>{{ gameEnd }}</h1>
    <h1>{{ result }}</h1>
    {{ formattedArr }}
    <div class="game-board">
      <div class="box" v-for="n in 9" @click="clicked(n - 1, player)" :key="n">
        <span v-if="formattedArr[n - 1] == 1"> O </span>

        <span v-if="formattedArr[n - 1] == 2"> X </span>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      player: 1,
      arr: [],
      gameEnd: false,
      result: "",
    };
  },
  created() {
    for (let index = 0; index < 9; index++) {
      this.arr.push(0);
    }
  },
  methods: {
    clicked: function (index, player) {
      if (this.gameEnd) return;

      if (this.arr[index] != 0) return;
      Vue.set(this.arr, index, player);
      if (++this.player > 2) this.player = 1;

      let aWin = this.haveWin(this.arr.map((x) => (x == 2 ? 0 : x)));
      let bWin = this.haveWin(this.arr.map((x) => (x == 1 ? 0 : x)));
      if (aWin) {
        this.gameEnd = true;
        return (this.result = "A WIN");
      }
      if (bWin) {
        this.gameEnd = true;
        return (this.result = "B WIN");
      }

      //Check if tie
      if (Math.min(...this.arr) > 0) {
        this.result = "TIE";
        return (this.gameEnd = true);
      }

      //Find if a winner exist here
    },
    haveWin: function (arr) {
      let winArr = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      for (let index = 0; index < winArr.length; index++) {
        const element = winArr[index];
        //if all 1
        let tmpArr = element.map((x) => arr[x]);
        if (!tmpArr.some((x) => x == 0)) return true;
      }

      return false;
    },
  },
  computed: {
    formattedArr: function () {
      return this.arr;
    },
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
  padding: 10px;
  grid-template-columns: repeat(3, 1fr);
}

.box {
  padding: 10px;
  display: table;
  background-color: lightblue;
}
.box > span {
  display: table-cell;
  vertical-align: middle;
}
</style>
