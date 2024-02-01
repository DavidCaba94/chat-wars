<template>
  <div class="chat-container" ref="chat">
    <div class="chat-header">
      <input class="input-channel" type="text" placeholder="ID del canal" v-model="channelID">
      <div class="btn-connect" @click="connectChat()">Connect</div>
      <div class="btn-disconnect" @click="disconnectChat()">Disconnect</div>
    </div>
    <div v-for="(msg, i) in chatHistory" :key="i">
      <div class="msg-box">
        <div class="time">{{msg.time.getHours() < 10 ? '0' + msg.time.getHours() : msg.time.getHours()}}:{{msg.time.getMinutes() < 10 ? '0' + msg.time.getMinutes() : msg.time.getMinutes()}}</div>
        <div v-if="msg.mod" class="mod-badge"></div>
        <div v-if="msg.sub" class="sub-badge"></div>
        <div class="msg-name" :style="{ color: msg.color ? msg.color : '#bb7cfd' }">{{msg.name}}:<span class="msg-txt">{{msg.txt}}</span></div>
      </div>
    </div>
  </div>
</template>

<script>
import tmi from "tmi.js"
export default {
  name: 'ChatBox',
  data() {
    return {
      channelID: '',
      chatHistory: [],
      client: null
    }
  },
  components: {
    
  },
  created() {
    
  },
  methods: {
    connectChat() {
      if (this.channelID !== '') {
        this.loadChat();
      }
    },
    disconnectChat() {
      if (this.client) {
        this.client.disconnect();
      }
    },
    loadChat() {
      this.client = new tmi.Client({
        channels: [ this.channelID ]
      });

      this.client.connect();

      this.client.on('message', (channel, tags, message, self) => {
        // console.log(`${channel}: ${self}`);
        // console.log(tags);
        let obj = {
          channel: channel,
          self: self,
          name: tags['display-name'],
          txt: message,
          color: tags['color'],
          mod: tags['mod'],
          sub: tags['subscriber'],
          time: new Date()
        };
        this.chatHistory.push(obj);
        this.scrollToBottom();
      });
    },
    scrollToBottom() {
      if (this.chatHistory.length > 0) {
        this.$refs.chat?.scrollTo(0, this.$refs.chat.scrollHeight);
      }
    }
  }
}
</script>
<style scoped>
.chat-container {
  position: fixed;
  width: 350px;
  height: calc(100vh - 90px);
  top: 50px;
  right: 0px;
  background-color: #282b30;
  padding: 20px 10px;
  padding-top: 60px;
  overflow: auto;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
  z-index: 8;
}

.chat-header {
  position: fixed;
  width: 350px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: nowrap;
  padding: 10px;
  top: 50px;
  right: 0px;
  background-color: #282b30;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
}

.input-channel {
  border: 0px;
  border-bottom: 1px solid #707377;
  color: #b4b4b4;
  background-color: #282b30;
  padding: 5px;
  outline: none;
}

.btn-connect {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 70px;
  height: 25px;
  border-radius: 5px;
  background-color: #bb7cfd;
  color: #ffffff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
  cursor: pointer;
}

.btn-connect:hover {
  background-color: #9d41ff;
}

.btn-disconnect {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 90px;
  height: 25px;
  border-radius: 5px;
  background-color: #fd7c7c;
  color: #ffffff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
  cursor: pointer;
}

.btn-disconnect:hover {
  background-color: #ff4a4a;
}

.msg-box {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  padding: 5px 10px;
  margin-bottom: 10px;
  font-size: 12px;
}

.time {
  font-weight: 300;
  color: #858585;
  margin-right: 8px;
}

.mod-badge {
  min-width: 10px;
  height: 10px;
  background-color: gold;
  border-radius: 50px;
  margin-right: 5px;
  margin-top: 2px;
}

.sub-badge {
  min-width: 10px;
  height: 10px;
  background-color: rgb(27, 219, 139);
  border-radius: 50px;
  margin-right: 5px;
  margin-top: 2px;
}

.msg-name {
  font-weight: bold;
  margin-right: 5px;
  text-align: left;
  line-height: 15px;
}

.msg-txt {
  font-weight: 300;
  color: #e2e2e2;
  margin-left: 5px;
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
</style>
