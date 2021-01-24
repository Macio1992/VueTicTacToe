<template>
  <section class="main">
    <div class="activePlayer">
      <h1 v-if="checkIfGameWon"> Player
        <span class="padding" :class="{ x: activePlayer === 'o', o: activePlayer === 'x' }">{{ activePlayer === 'x' ? 'o' : 'x' }}</span>
        wins! Congratulations</h1>
      <h1 v-else>Now
        <span class="padding" :class="{ x: activePlayer === 'x', o: activePlayer === 'o' }">{{ activePlayer }}</span>
        is choosing a cell
      </h1>
    </div>
    <div :class="{ isOver }" class="board">
      <div class="row" v-for="(row, i) in board" v-bind:key="row">
        <div
          :class="{ x: board[i][j] === 'x', o: board[i][j] === 'o' }"
          @click="showCoordinates(i, j)"
          class="cell" v-for="(cell, j) in row" v-bind:key="cell">
          {{ cell }}
        </div>
      </div>
    </div>
  </section>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data() {
      return {
        board: [
          ['', '', ''],
          ['', '', ''],
          ['', '', '']
        ],
        activePlayer: this.activePlayer === 'x' ? 'o' : 'x',
        isOver: false
      }
    },
    methods: {
      showCoordinates(i,j) {
        this.board[i][j] = this.activePlayer;
        this.activePlayer = this.activePlayer === 'x' ? 'o' : 'x';
      },
      checkRow(row, symbol) {
        return this.board[row][0] === symbol && this.board[row][1] === symbol && this.board[row][2] === symbol;
      },
      checkColumn(column, symbol) {
        return this.board[0][column] === symbol && this.board[1][column] === symbol && this.board[2][column] === symbol;
      },
      checkCrossFromLeft(symbol) {
        return this.board[0][0] === symbol && this.board[1][1] === symbol && this.board[2][2] === symbol;
      },
      checkCrossFromRight(symbol) {
        return this.board[0][2] === symbol && this.board[1][1] === symbol && this.board[2][0] === symbol;
      },
      setOverStatus() {
        this.isOver = true;
      }
    },
    computed: {
      checkIfGameWon() {
        if (this.checkRow(0, 'x') || this.checkRow(0, 'o')) {
          this.setOverStatus();
          return true;
        }

        if (this.checkRow(1, 'x') || this.checkRow(1, 'o')) {
          this.setOverStatus();
          return true;
        }

        if (this.checkRow(2, 'x') || this.checkRow(2, 'o')) {
          this.setOverStatus();
          return true;
        }

        if (this.checkColumn(0, 'x') || this.checkColumn(0, 'o')) {
          this.setOverStatus();
          return true;
        }

        if (this.checkColumn(1, 'x') || this.checkColumn(1, 'o')) {
          this.setOverStatus();
          return true;
        }

        if (this.checkColumn(2, 'x') || this.checkColumn(1, 'o')) {
          this.setOverStatus();
          return true;
        }

        if (this.checkCrossFromLeft('x') || this.checkCrossFromLeft('o')) {
          this.setOverStatus();
          return true;
        }

        if (this.checkCrossFromRight('x') || this.checkCrossFromRight('o')) {
          this.setOverStatus();
          return true;
        }

        return false;
      }
    }
  }
</script>

<style>
  body {
    font-family: Arial, Helvetica, sans-serif;
  }

  .padding {
    padding: 20px;
    border-radius: 2px;
  }

  .o {
    background-color: darkorange!important;
    color: white;
  }

  .x {
    background-color: forestgreen !important;
    color: white;
  }

  .isOver {
    pointer-events: none;
  }

  .main {
    display: flex;
    justify-content: space-between;
  }

  .board {
    width: 60%;
    display: flex;
    align-items: center;
    flex-direction: column;
  }

  .activePlayer {
    width: 40%;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .row {
    display: flex;
    width: 750px;
  }

  .cell {
    width: 250px;
    height: 250px;
    border: 1px solid;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    font-size: 50px;
    background-color: lightyellow;
  }
</style>
