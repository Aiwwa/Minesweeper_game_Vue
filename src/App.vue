<template>
  <h1>Minesweeper</h1>
  <button v-if="gameStarted" @click="startGame">Start game</button>
  <h3 v-if="gameOver">points: {{ points }}</h3>
  <div v-if="gameOver" class="game_over">
    <div>
      <p>Game Over</p>
      <p>Your score {{ points }}</p>
      <button @click="playAgain">Play again</button>
    </div>
  </div>
  <div class="game" :class="{ game_disabled: gameOver }">
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
      gameStarted: true,
      points: 0,
      game: [],
    }
  },
  methods: {
    handleCube(cube) {
      if (cube.bomb === true) {
        this.gameOver = true
        cube.bg = 'red'
      } else {
        this.points++
        cube.bg = 'green'
      }
    },
    play() {
      for (let i = 0; i < 100; i++) {
        this.game.push({ bomb: false, bg: 'gray' })
      }

      const random = () => {
        let x = Math.floor(Math.random() * 100)
        return x
      }

      for (let i = 0; i < 11; i++) {
        this.game[random()].bomb = true
      }
    },
    startGame() {
      this.play()
      this.gameStarted = false
    },
    playAgain() {
      this.gameOver = false
      this.points = 0
      this.game.forEach((el) => (el.bg = 'gray'))
      this.game = []
      this.gameStarted = true
    },
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: rgb(26, 26, 26);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #f9f9f9;
  margin-top: 60px;
  position: relative;
}

button {
  background-color: greenyellow;
  outline: none;
  border: none;
  padding: 20px 40px;
  margin-top: 40px;
}

.game {
  margin: 0 auto;
  width: 530px;
  display: flex;
  flex-wrap: wrap;
  margin-top: 100px;
}

h3 {
  margin: 30px 0;
}

.game_over {
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
  top: 800px;
  border: 1px solid greenyellow;
}

.game_disabled {
  cursor: not-allowed;
  pointer-events: none;
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
