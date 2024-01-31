<template>
  <div class="chat-container">
    <div v-for="(msg, i) in chatHistory" :key="i">
      <div class="msg-box">
        <div v-if="msg.mod" class="mod-badge"></div>
        <div v-if="msg.sub" class="sub-badge"></div>
        <div class="msg-name" :style="{ color: msg.color ? msg.color : '#000000' }">{{msg.name}}:</div>
        <div class="msg-txt">{{msg.txt}}</div>
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
        channels: [ '' ]
      });

      client.connect();

      client.on('message', (channel, tags, message, self) => {
        console.log(`${channel}: ${self}`);
        console.log(tags);
        let obj = {
          name: tags['display-name'],
          txt: message,
          color: tags['color'],
          mod: tags['mod'],
          sub: tags['subscriber']
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
  width: 300px;
  height: 100vh;
  top: 0px;
  right: 0px;
  background-color: #f5f5f5;
  padding: 5px;
}

.msg-box {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  padding: 5px;
  background-color: #ffffff;
  border-radius: 5px;
  margin-bottom: 5px;
  font-size: 12px;
}

.mod-badge {
  min-width: 10px;
  height: 10px;
  background-color: gold;
  border-radius: 50px;
  margin-right: 5px;
}

.sub-badge {
  min-width: 10px;
  height: 10px;
  background-color: rgb(27, 219, 139);
  border-radius: 50px;
  margin-right: 5px;
}

.msg-name {
  font-weight: bold;
  margin-right: 5px;
}

.msg-txt {
  font-weight: 300;
}
</style>
