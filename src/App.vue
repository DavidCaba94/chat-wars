<template>
  <ChatBox></ChatBox>
  <NavBar></NavBar>
  <MainMenu
    v-if="screenSelected === ''"
    @changeMenu="changeMenu">
  </MainMenu>
  <GameHangman
    v-if="screenSelected === 'GameHangman'"
    @changeMenu="changeMenu">
  </GameHangman>
  <GameMath
    v-if="screenSelected === 'GameMath'"
    @changeMenu="changeMenu">
  </GameMath>
  <GameWordle
    v-if="screenSelected === 'GameWordle'"
    @changeMenu="changeMenu">
  </GameWordle>
</template>

<script>
import ChatBox from './components/ChatBox.vue'
import NavBar from './components/NavBar.vue'
import MainMenu from './components/MainMenu.vue'
import GameHangman from './components/GameHangman.vue'
import GameMath from './components/GameMath.vue'
import GameWordle from './components/GameWordle.vue'

export default {
  name: 'App',
  components: {
    ChatBox,
    NavBar,
    MainMenu,
    GameHangman,
    GameMath,
    GameWordle
  },
  data() {
    return {
      screenSelected: ''
    }
  },
  methods: {
    changeMenu(selectedOption) {
      this.screenSelected = selectedOption;
      console.log(selectedOption);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  background-color: #121212;
}
</style>
