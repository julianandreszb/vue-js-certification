<script setup>
import ToeBox from '@/projects/TicTacToe/ToeBox.vue'
import { ref } from 'vue'

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
const currentPlayer = ref('X')
const board = Array.from({ length: 9 }, (v, i) => {
  return { index: i, player: null }
})
const isWinner = ref(false)

function checkWin() {
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
  if (checkWin()) {
    console.log(`${currentPlayer.value} wins!`)
    isWinner.value = true
  } else {
    currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X'
  }
}
</script>

<template>
  <section>
    <h1>Tic-tac-toe</h1>
    <p>{{ isWinner ? `Player ${currentPlayer} wins!` : `Player ${currentPlayer}'s turn` }}</p>
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
