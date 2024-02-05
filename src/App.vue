<template>
  <ChatBox
    @newMessage="newMessage">
  </ChatBox>
  <NavBar></NavBar>
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
    },
    newMessage(msg) {
      if (this.screenSelected === 'GameHangman') {
        this.$refs.GameHangman.newMessage(msg);
      } else if (this.screenSelected === 'GameMath') {
        this.$refs.GameMath.newMessage(msg);
      } else if (this.screenSelected === 'GameWordle') {
        this.$refs.GameWordle.newMessage(msg);
      }
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
