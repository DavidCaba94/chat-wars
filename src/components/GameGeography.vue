<template>
  <div class="game">
    <div class="close-game">
      <div class="btn-close">
        <img class="icon-close" src="../assets/icons/close.png" alt="Close" @click="changeMenu('')">
      </div>
    </div>
    <div class="game-area">

    </div>
  </div>
</template>

<script>
export default {
  name: 'GameGeography',
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
.game {
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

.close-game {
  width: calc(100% - 70px);
  display: flex;
  align-items: center;
  justify-content: flex-end;
  flex-wrap: nowrap;
}

.btn-close {
  width: 30px;
  height: 30px;
  background-color: #ff4848;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 5px;
  cursor: pointer;
}

.btn-close:hover {
  background-color: #e92a2a;
}

.icon-close {
  width: 25px;
}

.game-area {
  width: calc(100% - 60px);
  height: calc(100vh - 150px);
}
</style>
