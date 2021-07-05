<template>
  <div class="home">
    <div id="grid-container">
      <span
        class="cell"
        v-for="(n, i) in 900"
        :key="i"
        :data-x="Math.floor(i / 30) + 1"
        :data-y="(i % 30) + 1"
        @click="toggle($event.target)"
      >
      </span>
    </div>
    <nav>
      <button class="btn" @click="step()">Step</button>
      <button class="btn play" @click="auto()">Play</button>
      <button class="btn stop" @click="stop()">Stop</button>
      <button class="btn" @click="reset()">Reset</button>
    </nav>
  </div>
</template>

<script>
export default {
  data() {
    return {
      timer: "",
    };
  },
  methods: {
    toggle(cell) {
      if (cell.classList.contains("alive")) {
        cell.classList.remove("alive");
      } else {
        cell.classList.add("alive");
      }
    },
    setBehavior(f) {
      const gridCells = document.getElementById("grid-container").children;
      for (let cell of gridCells) {
        f(cell);
      }
    },
    checkNeighbors(cell) {
      let count = 0;
      const posX = Number(cell.dataset.x);
      const posY = Number(cell.dataset.y);
      if (
        cell.classList.contains("alive") &&
        (posX == 1 || posX == 30 || posY == 1 || posY == 30)
      ) {
        cell.dataset.neighbors = 0;
        return;
      }
      for (let r = -1; r <= 1; r++) {
        for (let c = -1; c <= 1; c++) {
          if (r === 0 && c === 0) {
            continue;
          }
          const adjX = posX + r;
          if (adjX === 0 || adjX === 31) {
            continue;
          }
          const adjY = posY + c;
          if (adjY === 0 || adjY === 31) {
            continue;
          }

          const adjCell = document.querySelector(
            `[data-x = '${adjX}'][data-y = '${adjY}']`
          );
          if (adjCell.classList.contains("alive")) {
            count++;
          }
        }
      }
      cell.dataset.neighbors = count;
    },
    setState(cell) {
      let state = cell.classList.contains("alive") ? "alive" : "dead";
      let n = Number(cell.dataset.neighbors);
      if (state === "alive") {
        if (n < 2 || n > 3) {
          cell.classList.remove("alive");
        }
      } else if (state === "dead") {
        if (n === 3) {
          cell.classList.add("alive");
        }
      }
    },
    step() {
      this.setBehavior(this.checkNeighbors);
      this.setBehavior(this.setState);
    },
    auto() {
      clearInterval(this.timer);
      this.timer = setInterval(this.step, 300);
    },
    stop() {
      clearInterval(this.timer);
    },
    reset() {
      this.setBehavior(this.resetGrid);
    },
    resetGrid(cell) {
      clearInterval(this.timer);
      cell.classList.remove("alive");
    },
  },
};
</script>

<style lang="scss">
$background-color: black;
$border-color: rgb(52, 58, 64);
$main-color: goldenrod;

.home {
  display: flex;
  min-height: 100vh;
  align-items: center;
  background-color: $background-color;
  #grid-container {
    display: grid;
    width: 70%;
    justify-content: center;
    grid-template-columns: repeat(30, 15px);
    grid-template-rows: repeat(30, 15px);
    grid-gap: 3px;
    .cell {
      border: 1px solid $border-color;
      border-radius: 3px;
      display: inline-block;
    }
    .alive {
      background-color: $main-color;
    }
  }
  nav {
    display: flex;
    flex-wrap: wrap;
    width: 30%;
    justify-content: center;
    padding: 0 2rem;
    .btn {
      background-color: $background-color;
      text-transform: uppercase;
      font-weight: bolder;
      color: $main-color;
      width: 100%;
      height: 2.5rem;
      border: 2px solid $main-color;
      &:active {
        transform: scale(0.97);
      }
    }
    .play,
    .stop {
      width: 50%;
    }
  }
}
</style>
