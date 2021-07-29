<template>
  <h1>Minesweeper</h1>
  <h3>points: {{ points }}</h3>
  <div v-if="gameOver" class="game_over">
    <div>
      <p>Game Over</p>
      <p>Your score {{ points }}</p>
      <button @click="playAgain">Play again</button>
    </div>
  </div>
  <div class="game">
    <div
      v-for="cube in game"
      :key="cube.bomb"
      class="cube"
      @click="handleCube(cube)"
      :style="{ background: cube.bg }"
    ></div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      gameOver: false,
      points: 0,
      game: [],
    }
  },
  methods: {
    handleCube(cube) {
      if (cube.bomb === true) {
        this.gameOver = true
      } else {
        this.points++
        console.log(cube)
        cube.bg = 'green'
      }
    },
    playAgain() {
      this.gameOver = false
      this.points = 0
      this.game.forEach((el) => (el.bg = 'gray'))
    },
  },
  components: {},
  mounted() {
    for (let i = 0; i < 100; i++) {
      this.game.push({ bomb: false, bg: 'gray' })
    }

    const random = () => {
      let x = Math.floor(Math.random() * 100)
      console.log(x)

      return x
    }

    for (let i = 0; i < 11; i++) {
      this.game[random()].bomb = true
    }

    console.log(this.game)
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  position: relative;
}

.game {
  margin: 0 auto;
  width: 530px;
  display: flex;
  flex-wrap: wrap;
}

h3 {
  margin: 30px 0;
}

.game_over {
  background-color: rgb(0, 0, 0);
  color: white;
  width: 510px;
  height: 200px;
  padding: 30px;
  position: absolute;
  left: calc(50% - 270px);
  font-weight: 900;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  padding: 10px;
}

.game_over p:nth-child(1) {
  color: red;
  font-size: 24px;
  margin: 20px 0;
}

.game_over button {
  margin-top: 40px;
  margin-bottom: 20px;
  padding: 10px 20px;
  background-color: rgb(244, 212, 171);
  border: none;
}

.cube {
  width: 50px;
  height: 50px;
  background-color: rgb(145, 145, 145);
  background-color: gray;
  border: 1px solid black;
}
</style>
