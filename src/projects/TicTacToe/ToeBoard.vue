<script setup>
import ToeBox from '@/projects/TicTacToe/ToeBox.vue'
import { reactive, ref } from 'vue'

const combinations = [
  [0, 1, 2],
  [0, 4, 8],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8],
  [2, 4, 6],
  [3, 4, 5],
  [6, 7, 8]
]

function fillBoard(board) {
  Array.from({ length: 9 }, (v, i) => {
    const box = { index: i, player: null }
    board.push(box)
    return box
  })
}
function clearBoard(board) {
  board.splice(0)
}
const board = reactive([])
fillBoard(board)

const currentPlayer = ref('X')
const isWinner = ref(false)
const isDraw = ref(false)
const isNewGameButtonVisible = ref(false)

function startNewGame() {
  clearBoard(board)
  fillBoard(board)
  currentPlayer.value = 'X'
  isDraw.value = false
  isWinner.value = false
  isNewGameButtonVisible.value = false
}

function isDrawGame() {
  for (const box of board) {
    if (box.player === null) {
      return false
    }
  }
  return true
}

function isWin() {
  for (const combination of combinations) {
    let hitsCounter = 0
    for (const index of combination) {
      if (board[index].player === currentPlayer.value && board[index].player !== null) {
        hitsCounter++
      } else {
        break
      }

      if (hitsCounter === 3) {
        return true
      }
    }
  }
}

function updateBox(box) {
  board[box.index].player = currentPlayer.value

  isDraw.value = isDrawGame()
  isWinner.value = isWin()

  if (isDraw.value || isWinner.value) {
    isNewGameButtonVisible.value = true
    return
  }

  currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X'
}
</script>

<template>
  <section>
    <h1>Tic-tac-toe</h1>
    <p v-if="isWinner">{{ `Player ${currentPlayer} wins!` }}</p>
    <p v-else-if="isDraw">{{ `Draw!` }}</p>
    <p v-else>{{ `Player ${currentPlayer}'s turn` }}</p>
    <button type="button" v-if="isNewGameButtonVisible" @click="startNewGame">New Game</button>
    <article>
      <div class="grid">
        <ToeBox
          class="cell"
          v-for="box in board"
          :box="box"
          :currentPlayer="currentPlayer"
          :key="box"
          @updateBox="updateBox"
          >{{ box.index }}</ToeBox
        >
      </div>
    </article>
  </section>
</template>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  max-width: 150px;
}

.cell {
  border: 1px solid #000;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
}

h1 {
  text-align: center;
}
</style>
