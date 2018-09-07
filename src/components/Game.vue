<template lang="html">
  <div class="container">
    <div class="row d-flex justify-content-center">
      <div class="col" style="max-width: 300px;">
        <div class="row mt-3">
          <div @click="userMove(0)" class="col-4 square sq0 d-flex justify-content-center align-items-center display-4">
            <span v-show="squares[0].X">X</span>
            <span v-show="squares[0].O">O</span>
          </div>
          <div @click="userMove(1)" class="col-4 square sq1 d-flex justify-content-center align-items-center display-4">
            <span v-show="squares[1].X">X</span>
            <span v-show="squares[1].O">O</span>
          </div>
          <div @click="userMove(2)" class="col-4 square sq2 d-flex justify-content-center align-items-center display-4">
            <span v-show="squares[2].X">X</span>
            <span v-show="squares[2].O">O</span>
          </div>
        </div>
        <div class="row">
          <div @click="userMove(3)" class="col-4 square sq3 d-flex justify-content-center align-items-center display-4">
            <span v-show="squares[3].X">X</span>
            <span v-show="squares[3].O">O</span>
          </div>
          <div @click="userMove(4)" class="col-4 square sq4 d-flex justify-content-center align-items-center display-4">
            <span v-show="squares[4].X">X</span>
            <span v-show="squares[4].O">O</span>
          </div>
          <div @click="userMove(5)" class="col-4 square sq5 d-flex justify-content-center align-items-center display-4">
            <span v-show="squares[5].X">X</span>
            <span v-show="squares[5].O">O</span>
          </div>
        </div>
        <div class="row">
          <div @click="userMove(6)" class="col-4 square sq6 d-flex justify-content-center align-items-center display-4">
            <span v-show="squares[6].X">X</span>
            <span v-show="squares[6].O">O</span>
          </div>
          <div @click="userMove(7)" class="col-4 square sq7 d-flex justify-content-center align-items-center display-4">
            <span v-show="squares[7].X">X</span>
            <span v-show="squares[7].O">O</span>
          </div>
          <div @click="userMove(8)" class="col-4 square sq8 d-flex justify-content-center align-items-center display-4">
            <span v-show="squares[8].X">X</span>
            <span v-show="squares[8].O">O</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      probabilities: [],
      state: [.5, .5, .5, .5, .5, .5, .5, .5, .5],
      squares: [
          {
            X: false,
            O: false
          },
          {
            X: false,
            O: false
          },
          {
            X: false,
            O: false
          },
          {
            X: false,
            O: false
          },
          {
            X: false,
            O: false
          },
          {
            X: false,
            O: false
          },
          {
            X: false,
            O: false
          },
          {
            X: false,
            O: false
          },
          {
            X: false,
            O: false
          }
      ]
    }
  },

  created () {
    this.nextMove()
  },

  methods: {
    gameWon () {
      switch(this.state[0], this.state[1], this.state[2]) {
        case 0, 0, 0:
          alert('Game over!')
          break
      }
    },
    async nextMove () {
      this.probabilities.length = 0
      let array = this.state.slice()
      for (let i = 0; i < 9; i++) {
        if (array[i] === .5) {
          array.splice(i, 1, 1)
        }
        let res = await axios.post('http://localhost:3000/get-result', {
          array: array
        })
        this.probabilities.push(res.data.Result[0])
        array = this.state.slice()
      }
      let highestProb = Math.max(...this.probabilities)
      let index = this.probabilities.indexOf(highestProb)
      this.squares[index].X = true
      this.state.splice(index, 1, 1)
    },
    userMove (n) {
      this.squares[n].O = true
      this.state.splice(n, 1, 0)
      setTimeout(() => {
        this.nextMove()
      }, 1000)
    }
  }
}
</script>

<style lang="css">
.square {
  max-width: 100px;
  height: 100px;
}
.square:hover {
  background-color: #ccf4ff;
  cursor: pointer;
}
.sq0, .sq1, .sq3, .sq4 {
  border-right: solid black;
  border-bottom: solid black;
}
.sq2, .sq5 {
  border-bottom: solid black;
}
.sq6, .sq7 {
  border-right: solid black;
}
</style>
