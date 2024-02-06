<template>
  <ChatBox
    @newMessage="newMessage">
  </ChatBox>
  <NavBar
    @changeMenu="changeMenu">
  </NavBar>
  <MainMenu
    v-if="screenSelected === ''"
    @changeMenu="changeMenu">
  </MainMenu>
  <GameHangman
    ref="GameHangman"
    v-if="screenSelected === 'GameHangman'"
    @changeMenu="changeMenu">
  </GameHangman>
  <GameMath
    ref="GameMath"
    v-if="screenSelected === 'GameMath'"
    @changeMenu="changeMenu">
  </GameMath>
  <GameWordle
    ref="GameWordle"
    v-if="screenSelected === 'GameWordle'"
    @changeMenu="changeMenu">
  </GameWordle>
  <GameGeography
    ref="GameGeography"
    v-if="screenSelected === 'GameGeography'"
    @changeMenu="changeMenu">
  </GameGeography>
  <GameFlags
    ref="GameFlags"
    v-if="screenSelected === 'GameFlags'"
    @changeMenu="changeMenu">
  </GameFlags>
</template>

<script>
import ChatBox from './components/ChatBox.vue'
import NavBar from './components/NavBar.vue'
import MainMenu from './components/MainMenu.vue'
import GameHangman from './components/GameHangman.vue'
import GameMath from './components/GameMath.vue'
import GameWordle from './components/GameWordle.vue'
import GameGeography from './components/GameGeography.vue'
import GameFlags from './components/GameFlags.vue'

export default {
  name: 'App',
  components: {
    ChatBox,
    NavBar,
    MainMenu,
    GameHangman,
    GameMath,
    GameWordle,
    GameGeography,
    GameFlags
  },
  data() {
    return {
      screenSelected: ''
    }
  },
  methods: {
    changeMenu(selectedOption) {
      this.screenSelected = selectedOption;
    },
    newMessage(msg) {
      if (this.screenSelected === 'GameHangman') {
        this.$refs.GameHangman.newMessage(msg);
      } else if (this.screenSelected === 'GameMath') {
        this.$refs.GameMath.newMessage(msg);
      } else if (this.screenSelected === 'GameWordle') {
        this.$refs.GameWordle.newMessage(msg);
      } else if (this.screenSelected === 'GameGeography') {
        this.$refs.GameWordle.newMessage(msg);
      }
    }
  }
}
</script>

<style>
html {
  background-color: #424549;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  background-color: #121212;
}
</style>
