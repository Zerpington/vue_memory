<template>
  <div id="app">

    <div class="game-header" v-if="!gameStarted">
      <h1>Vue Memory Game</h1>

      <div id="start-game" @click="startGame">
        START
      </div>

    </div>

    <div id="card-container" v-if="gameStarted">
      <div class="card-row">
        <div class="card-column" @click="firstOne">{{ fOne }}</div>
        <div class="card-column" @click="firstTwo">{{ fTwo }}</div>
        <div class="card-column" @click="firstThree">{{ fThree }}</div>
        <div class="card-column" @click="firstFour">{{ fFour }}</div>
      </div>
      <div class="card-row">
        <div class="card-column" @click="secondOne">{{ sOne }}</div>
        <div class="card-column" @click="secondTwo">{{ sTwo }}</div>
        <div class="card-column" @click="secondThree">{{ sThree }}</div>
        <div class="card-column" @click="secondFour">{{ sFour }}</div>
      </div>
      <div class="card-row">
        <div class="card-column" @click="firstFive">{{ fFive }}</div>
        <div class="card-column" @click="firstSix">{{ fSix }}</div>
        <div class="card-column" @click="firstSeven">{{ fSeven }}</div>
        <div class="card-column" @click="firstEight">{{ fEight }}</div>
      </div>
      <div class="card-row">
        <div class="card-column" @click="secondFive">{{ sFive }}</div>
        <div class="card-column" @click="secondSix">{{ sSix }}</div>
        <div class="card-column" @click="secondSeven">{{ sSeven }}</div>
        <div class="card-column" @click="secondEight">{{ sEight }}</div>
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
      memoryNum: null,
      fOne: null,
      fTwo:null,
      fThree:null,
      fFour:null,
      fFive:null,
      fSix:null,
      fSeven:null,
      fEight:null,
      sOne:null,
      sTwo:null,
      sThree:null,
      sFour:null,
      sFive:null,
      sSix:null,
      sSeven:null,
      sEight:null,
    }
  },

  methods: {
    startGame () {
      this.gameStarted = true
      this.shuffleCards()
    },
    endGame () {
      this.gameStarted = false
    },

    //shuffleCards () {
    //var cards = (".card-column");
    //  for(var i = 0; i < cards.length; i++) {
    //      var target = Math.floor(Math.random() * cards.length -1) + 1;
    //      var target2 = Math.floor(Math.random() * cards.length -1) + 1;
    //      $(":cards.eq(target)".before(":cards.eq(target2)")
    //  }
    //},

    firstOne () {
      if(this.fOne == null){
        this.fOne = 1
      } else {
        this.fOne = null
      }

    },
    secondOne () {
      if(this.sOne == null){
        this.sOne = 1
      } else {
        this.sOne = null
      }
    },
    firstTwo () {
      if(this.fTwo == null){
        this.fTwo = 2
      } else {
        this.fTwo = null
      }
    },
    secondTwo () {
      if(this.sTwo == null){
        this.sTwo = 1
      } else {
        this.sTwo = null
      }
    },
    firstThree (){
      this.fThree =3

    },
    secondThree () {
      this.sThree =3

    },
    firstFour (){
      this.fFour =4
    },
    secondFour () {
      this.sFour =4

    },
    firstFive () {
      this.fFive =5

    },
    secondFive () {
      this.sFive =5

    },
    firstSix () {
      this.fSix =6

    },
    secondSix () {
      this.sSix =6

    },
    firstSeven () {
      this.fSeven =7

    },
    secondSeven () {
      this.sSeven =7

    },
    firstEight () {
      this.fEight =8

    },
    secondEight () {
      this.sEight =8

    },

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.game-header {
  position: relative;
  align-items: center;
  margin: auto;
  top: 50%;
  background-color: antiquewhite;
  border-radius: 1em;
  width: 350px;
  height: auto;
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
