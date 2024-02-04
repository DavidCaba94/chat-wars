<template>
  <div class="menu">
    <div class="game-card-container">
      <div class="game-card color-1" @click="changeMenu('GameHangman')">
        <img class="card-icon" src="../assets/icons/hangman.png" alt="Hangman">
      </div>
      <div class="game-card-title">Ahorcado</div>
    </div>
    <div class="game-card-container">
      <div class="game-card color-2" @click="changeMenu('GameMath')">
        <img class="card-icon" src="../assets/icons/math.png" alt="Math">
      </div>
      <div class="game-card-title">Math</div>
    </div>
    <div class="game-card-container">
      <div class="game-card color-3" @click="changeMenu('GameWordle')">
        <img class="card-icon" src="../assets/icons/wordle.png" alt="Wordle">
      </div>
      <div class="game-card-title">Wordle</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainMenu',
  data() {
    return {
      
    }
  },
  methods: {
    changeMenu(selectedOption) {
      this.$emit('changeMenu', selectedOption);
    }
  }
}
</script>

<style scoped>
.menu {
  position: fixed;
  width: calc(100% - 350px);
  height: calc(100vh - 50px);
  background-color: #424549;
  top: 50px;
  left: 0px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  flex-wrap: wrap;
  padding: 20px;
}

.game-card-container {
  width: 250px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
}

.game-card {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 200px;
  height: 160px;
  border-radius: 10px;
  cursor: pointer;
}

.game-card.color-1 {
  background-color: #bb7cfd;
}

.game-card.color-1:hover {
  background-color: #9d5ce2;
}

.game-card.color-2 {
  background-color: #fdea7c;
}

.game-card.color-2:hover {
  background-color: #fae04a;
}

.game-card.color-3 {
  background-color: #9afd7c;
}

.game-card.color-3:hover {
  background-color: #6edb4c;
}

.game-card-title {
  margin-top: 10px;
  font-weight: bold;
}

.card-icon {
  width: 90px;
  opacity: 0.5;
}
</style>
