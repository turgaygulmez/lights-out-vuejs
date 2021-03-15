<template>
  <div class="wrapper">
    <div class="result">
      {{ !isFailed ? "Congrats! you completed it" : "Keep pushing" }}
    </div>
    <button class="btn" v-on:click="restart">Restart</button>
    <div
      class="board-container"
      v-bind:style="{
        width: this.baseSize.width,
        height: this.baseSize.height,
      }"
    >
      <div class="row" v-for="column in grid" :key="column.id">
        <div
          class="row-item"
          v-for="row in column"
          v-bind:class="[row.lightOn ? 'light-on' : 'light-off']"
          v-on:click="toggle"
          :key="row.id"
          :data-coordinateX="row.coordinateX"
          :data-coordinateY="row.coordinateY"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LightOnBoard",
  props: {
    size: Number,
    lightOnCount: Number,
  },
  data() {
    return {
      grid: null,
      isFailed: true,
    };
  },
  created: function () {
    this.initGrid();
    this.randomizeLight();
  },
  computed: {
    baseSize: function () {
      return {
        width: this.size * 50 + "px",
        height: this.size * 50 + "px",
      };
    },
  },
  methods: {
    initGrid: function () {
      const grid = Array(this.size);
      for (let y = 0; y < grid.length; y++) {
        grid[y] = Array(this.size);
        for (let x = 0; x < grid[y].length; x++) {
          grid[y][x] = {
            lightOn: false,
            coordinateY: y,
            coordinateX: x,
          };
        }
      }
      this.grid = grid;
    },
    restart: function () {
      this.initGrid();
      this.randomizeLight();
      this.failed = true;
    },
    randomizeLight: function () {
      for (let index = 0; index < this.lightOnCount; index++) {
        var x = Math.floor(Math.random() * Math.floor(this.size));
        var y = Math.floor(Math.random() * Math.floor(this.size));

        this.grid[x][y].lightOn = true;
      }
    },
    toggle: function (event) {
      const data = event.target.dataset;
      const y = parseInt(data.coordinatey);
      const x = parseInt(data.coordinatex);

      this.grid[y][x].lightOn = !this.grid[y][x].lightOn;

      const directions = [
        [1, 0],
        [-1, 0],
        [0, 1],
        [0, -1],
      ];

      for (let direction of directions) {
        let targetY = y + direction[0];
        let targetX = x + direction[1];
        if (
          targetY >= 0 &&
          targetY < this.size &&
          targetX >= 0 &&
          targetX < this.size
        ) {
          this.grid[targetY][targetX].lightOn = !this.grid[targetY][targetX]
            .lightOn;
        }
      }

      this.isFailed = this.checkIsFailed();
    },
    checkIsFailed: function () {
      let failed = false;
      for (let y = 0; y < this.grid.length; y++) {
        if (failed) {
          break;
        }

        for (let x = 0; x < this.grid[y].length; x++) {
          if (!this.grid[y][x].lightOn) {
            failed = true;
            break;
          }
        }
      }

      return failed;
    },
  },
};
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.result {
  font-size: 1.5rem;
}

.board-container {
  display: flex;
  flex-direction: column;
}

.row {
  display: flex;
}

.row-item {
  width: 50px;
  height: 50px;
  display: flex;
  flex-direction: row;
  transition: all 0.3s;
  box-shadow: rgba(255, 255, 255, 0.2) 0px 0px 0px 1px inset,
    rgba(0, 0, 0, 0.9) 0px 0px 0px 1px;
}

.row-item:hover {
  cursor: pointer;
}

.row-item.light-on {
  background: rgb(104, 243, 11);
}

.row-item.light-off {
  background: rgb(1, 61, 1);
}

.btn {
  position: relative;
  display: block;
  margin: 1rem auto;
  padding: 1rem;
  overflow: hidden;
  border-width: 0;
  outline: none;
  border-radius: 2px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.6);
  background-color: #2ecc71;
  color: #ecf0f1;
  transition: background-color 0.3s;
}

.btn:hover,
.btn:focus {
  background-color: #27ae60;
}
</style>
