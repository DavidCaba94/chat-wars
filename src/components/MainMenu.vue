<template>
  <div class="menu">
    <div class="game-card-container">
      <div class="game-card color-1">
        
      </div>
      <div class="game-card-title">Ahorcado</div>
    </div>
    <div class="game-card-container">
      <div class="game-card color-2">
        
      </div>
      <div class="game-card-title">Math</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainMenu'
}
</script>

<style scoped>
.menu {
  position: fixed;
  width: 100%;
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
  width: 300px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
}

.game-card {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 250px;
  height: 200px;
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

.game-card-title {
  margin-top: 10px;
  font-weight: bold;
}
</style>
