<template>
  <ChatBox></ChatBox>
  <NavBar></NavBar>
  <MainMenu></MainMenu>
</template>

<script>
import ChatBox from './components/ChatBox.vue'
import NavBar from './components/NavBar.vue'
import MainMenu from './components/MainMenu.vue'

export default {
  name: 'App',
  components: {
    ChatBox,
    NavBar,
    MainMenu
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
