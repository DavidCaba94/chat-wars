<template>
  <div class="game">
    <div class="close-game">
      <div class="btn-close">
        <img class="icon-close" src="../assets/icons/close.png" alt="Close" @click="changeMenu('')">
      </div>
    </div>
    <div class="game-area">
      <div class="ahorcado">
        <div class="tiles-container">
          <div :class="letter === discovered[index] ? 'letra-correcta' : 'letra'" v-for="(letter, index) in letters" :key="index">
            {{letter === discovered[index] ? letter : ''}}
          </div>
        </div>
        <div class="fails-title">Fails: {{fails.length}}/15</div>
        <div class="tiles-container">
          <div class="letra-incorrecta" v-for="(fail, index) in fails" :key="index">{{fail}}</div>
        </div>
      </div>
      <div class="baneados">
        <div class="ban-title">BAN LIST</div>
        <div class="ban-list" ref="banList">
          <div class="banned-box" v-for="banned in banneds" :key="banned">{{banned}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import diccionario from '../assets/json/diccionario.json'
export default {
  name: 'GameHangman',
  data() {
    return {
      word: '',
      letters: [],
      discovered: [],
      banneds: [],
      fails: [],
      winner: null
    }
  },
  created() {
    this.getRandomWord();
  },
  methods: {
    changeMenu(selectedOption) {
      this.$emit('changeMenu', selectedOption);
    },
    getRandomWord() {
      let tempWord = '';
      while (tempWord.length < 4) {
        let randomNumber = Math.floor(Math.random() * 5000);
        tempWord = diccionario.words[randomNumber];
      }
      this.word = tempWord.toUpperCase();
      for (var i = 0; i < this.word.length; i++) {
        this.letters.push(this.checkAccents(this.word.charAt(i).toUpperCase()));
        this.discovered.push('');
      }
    },
    checkAccents(letter) {
      let ltr = letter;
      switch (ltr) {
        case 'Á':
          ltr = 'A';
          break;
        case 'É':
          ltr = 'E';
          break;
        case 'Í':
          ltr = 'I';
          break;
        case 'Ó':
          ltr = 'O';
          break;
        case 'Ú':
        case 'Ü':
          ltr = 'U';
          break;
      }
      return ltr;
    },
    newMessage(msg) {
      if (this.winner === null && this.fails.length < 15 && !this.banneds.includes(msg.name)) {
        this.checkNewMessage(msg);
      }
    },
    checkNewMessage(msg) {
      if (msg.txt.length === 1) {
        if (!this.discovered.includes(msg.txt.toUpperCase()) && this.letters.includes(msg.txt.toUpperCase())) {
          this.discovered.push(msg.txt.toUpperCase());
        } else if (!this.discovered.includes(msg.txt.toUpperCase()) && !this.letters.includes(msg.txt.toUpperCase())) {
          this.banneds.push(msg.name);
          if (!this.fails.includes(msg.txt.toUpperCase())) this.fails.push(msg.txt.toUpperCase());
        }
      } else {
        if (msg.txt.toUpperCase() === this.word) {
          this.winner = msg;
          this.discovered = this.letters;
        } else {
          this.banneds.push(msg.name);
        }
      }
      this.$refs.banList?.scrollTo(0, this.$refs.banList.scrollHeight);
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
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  flex-wrap: nowrap;
}

.ahorcado {
  width: 70%;
  padding: 10px;
}

.baneados {
  width: 30%;
  padding: 10px;
}

.tiles-container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: nowrap;
}

.letra {
  width: 70px;
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 36px;
  font-weight: bold;
  color: #ffffff;
  border: 1px solid #ffffff;
  border-radius: 10px;
  margin-left: 10px;
}

.letra-correcta {
  width: 70px;
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 36px;
  font-weight: bold;
  color: #ffffff;
  border: 1px solid #ffffff;
  border-radius: 10px;
  margin-left: 10px;
  background-color: #56b938;
}

.fails-title {
  margin-top: 80px;
  margin-bottom: 50px;
  font-size: 32px;
  font-weight: bold;
}

.letra-incorrecta {
  width: 70px;
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 36px;
  font-weight: bold;
  color: #ffffff;
  border: 1px solid #ffffff;
  border-radius: 10px;
  margin-left: 10px;
  background-color: #ff4040;
}

.ban-title {
  margin-bottom: 30px;
  font-size: 32px;
  font-weight: bold;
}

.ban-list {
  height: calc(100vh - 265px);
  overflow: auto;
  padding: 10px;
  padding-bottom: 35px;
}

/* width */
::-webkit-scrollbar {
  width: 7px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #282b30; 
}
 
/* Handle */
::-webkit-scrollbar-thumb {
  background: #707377;
  border-radius: 10px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #707377; 
}

.banned-box {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: nowrap;
  padding: 5px;
  background-color: #707377;
  font-weight: 700;
  margin-bottom: 5px;
  border-radius: 5px;
}
</style>
