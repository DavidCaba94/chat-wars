<template>
  <div class="nav-bar">
    <div class="first-items">
      <img class="icon" src="../assets/logo.png" alt="Chat Wars" @click="goToMenu()">
      <div class="menu-title">Chat Wars</div>
    </div>
    <div class="last-items">
      <img class="icon" src="../assets/icons/info.png" alt="Info" @click="showInfo()">
    </div>
  </div>
</template>

<script>
export default {
  name: 'NavBar',
  data() {
    return {
        
    }
  },
  methods: {
    goToMenu() {

    },
    showInfo() {

    }
  }
}
</script>

<style scoped>
.nav-bar {
  position: fixed;
  width: 100%;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: nowrap;
  background-color: #1e2124;
  top: 0px;
  left: 0px;
  z-index: 9;
}

.first-items {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  flex-wrap: nowrap;
}

.last-items {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  flex-wrap: nowrap;
  margin-right: 20px;
}

.icon {
  width: 40px;
  margin-left: 20px;
  cursor: pointer;
}

.menu-title {
  font-size: 32px;
  font-weight: bold;
  margin-left: 20px;
  color: #ffffff;
}
</style>
