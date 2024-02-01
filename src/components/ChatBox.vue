<template>
  <div class="chat-container">
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
      chatHistory: []
    }
  },
  components: {
    
  },
  created() {
    this.loadChat();
  },
  methods: {
    loadChat() {
      const client = new tmi.Client({
        channels: [ 'IlloJuan' ]
      });

      client.connect();

      client.on('message', (channel, tags, message, self) => {
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
      });
    }
  }
}
</script>
<style scoped>
.chat-container {
  position: fixed;
  width: 350px;
  height: calc(100vh - 50px);
  top: 50px;
  right: 0px;
  background-color: #282b30;
  padding: 10px;
  overflow: auto;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
  z-index: 8;
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
</style>
