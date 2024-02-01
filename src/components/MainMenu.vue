<template>
  <div class="menu">
    <div class="game-card">
      Ahorcado
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
  align-items: center;
  justify-content: flex-start;
  flex-wrap: wrap;
}
</style>
