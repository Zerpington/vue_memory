<template>
  <div id="app">

    <div class="game-title">Vue Memory Game</div>

    <div class="game-container">
      <div
        id="start-game"
        @click="startGame"
        v-if="!gameStarted"
      >
        START
      </div>

      <div class="difficulty-container" v-if="gameStarted && chooseDifficulty">
        <div class="button green" @click="setDifficulty('easy')">
          Easy (4 x 4)
        </div>
        <div class="button blue" @click="setDifficulty('medium')">
          Medium (6 x 6)
        </div>
        <div class="button red" @click="setDifficulty('hard')">
          Hard (8 x 8)
        </div>
      </div>

      <div class="end-game" @click="startGame" v-if="wonGame">
        <div>
          <img src="../chika.gif">
        </div>
        Play Again?
      </div>

      <div :class="difficultyClass" v-if="gameStarted && !chooseDifficulty">
        <div
          v-for="(card, index) in memoryCards" :key="index"
          class="memory-card"
        >
          <div v-if="cardMask[index]">
            {{ card }}
          </div>

          <div
            class="covered-card"
            v-if="!cardMask[index]"
            @click="unmaskCard(index)"
          />
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'App',

  data: function () {
    return {
      gameStarted: false,
      chooseDifficulty: false,
      memoryCards: [],
      cardMask: [],
      difficulty: "easy",
      unmaskStack: [],
      wonGame: false,
      openCards: 0,
      winBanner: null,
    }
  },

  computed: {
    difficultyClass () {
      if (this.difficulty === "easy"){
        return "small-board game-board"
      } else if (this.difficulty === "medium") {
        return "medium-board game-board"
      } else {
        return "large-board game-board"
      }
    }
  },

  methods: {
    startGame () {
      this.gameStarted = true
      this.chooseDifficulty = true
      this.wonGame = false
      this.openCards = 0

    },

    endGame () {
      this.gameStarted = false
    },

    setDifficulty(difficulty) {
      this.chooseDifficulty = false
      this.difficulty = difficulty

      if (difficulty === "easy") {
        this.inititalizeCards(16)
      } else if (difficulty === "medium") {
        this.inititalizeCards(36)
      } else if (difficulty === "hard") {
        this.inititalizeCards(64)
      }
    },

    inititalizeCards(number) {
      const cards = []
      const mask = []
      for (let i = 1; i <= number/2; i++) {
        cards.push(i)
        cards.push(i)
        mask.push(false)
        mask.push(false)
      }

      const SHUFFLE_COUNT = 4

      for (let i = 0; i < SHUFFLE_COUNT; i++) {
        for (let j = 0; j < number; j++) {
          const rand = Math.floor((Math.random() * number))
          const temp = cards[rand]
          cards[rand] = cards[j]
          cards[j] = temp
        }
      }

      this.memoryCards = cards
      this.cardMask = mask
    },

    unmaskCard(index) {


      if (this.unmaskStack.length === 2) {
        const x = this.unmaskStack[0]
        const y = this.unmaskStack[1]
        if (this.memoryCards[x] != this.memoryCards[y]) {
          for (let i = 0; i < this.unmaskStack.length; i++) {
            const index = this.unmaskStack[i]
            this.$set(this.cardMask, index, false)
          }
        }
      }
      if (this.unmaskStack.length > 1) {
        this.unmaskStack = []
      }
      this.$set(this.cardMask, index, true)
      this.unmaskStack.push(index)
      this.winCondtion()
    },

    winCondtion(){
      this.openCards = 0
      for (let i = 0; i < this.cardMask.length; i++){
        if(this.cardMask[i] == true){
          this.openCards++

          }
      if (this.openCards == this.cardMask.length) {
        this.wonGame = true

        }
      }

    },

  }
}
</script>

<style>
html, body {
  margin: 0;
  height: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: antiquewhite;
  height: 100%;

  display: flex;
  flex-direction: column;
}

.end-game {
  position: absolute;
  display: flex;
  flex-direction: column;
  height: auto;
  width: auto;
  background-color: pink;
  padding: 10px;
  font-size: 20px;
  border: solid;
  border-radius: .5em;
  color: green;
}

.game-title {
  font-size: 2em;
  font-weight: 300;
  padding-top: 1em;
}

.game-container {
  display: flex;
  flex-grow: 1;
  justify-content: center;
}

.difficulty-container {
  display: flex;
  align-items: center;
}

.red {
  background-color: red;
  color: white
}

.green {
  background-color: green;
  color: white;
}

.blue {
  background-color: blue;
  color: white;
}

.button {
  padding: 1em;
  margin: 10px;
  border-radius: 0.5em;
}

.button:hover {
  cursor: pointer;
  background-color: rgba(0,0,0,0.4);
}

.game-board {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.small-board {
  width: 500px;
}

.medium-board {
  width: 700px;
}

.large-board {
  width: 900px;
}

.memory-card {
  width: 100px;
  margin: 5px;
  border: 1px solid black;
  border-radius: 10px;

  display: flex;
  align-items: center;
  justify-content: center;
}

.memory-card:hover {
  cursor: pointer;
}

.covered-card {
  background-color: pink;
  width: 100px;
  height: 100%;
  border-radius: 10px;
}

#start-game {
  margin: auto;
  width: 150px;
  font-size: 25px;
  padding: 5px;
  background-color: whitesmoke;
  border-radius: 1em;
  border: 1px solid black;
}

#start-game:hover {
  cursor: pointer;
  background-color: cornsilk;
}

#card-container{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content:center;
  align-content: space-between;
}

.card-row{
  display: flex;
  flex-direction: row;
  font-size: 50px;

}

.card-column{
  height: 150px;
  width: 100px;
  border: 1px solid black;

}

.card-column:hover{
  background-color: gray;
  cursor: pointer;
}

</style>
