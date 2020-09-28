<template>
  <div class="flex live-box">
    <div class="content">
      <div class="live-item" v-for="live of liveList" :key="live.text">
        <span>{{ live.text }}</span>
        <span>{{ live.score }}</span>
      </div>
      <div class="live-item" v-if="!liveList.length">比赛尚未开始！</div>
    </div>
    <div class="input-bar">
      <input placeholder="畅所欲言..." v-model="inputValue" v-on:keyup.enter="onSend()" />
      <button type="button" @click='onSend()'>发送</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LiveBox',
  data() {
    return {
      liveList: [],
      inputValue: '',
      ws: new WebSocket("wss://echo.websocket.org")
    }
  },
  methods: {
    onSend: function() {
      this.ws.send(this.inputValue);
      this.inputValue = '';
    }
  },
  created() {
    this.ws.onopen = function() {
      console.log('Connection open...');
    }
    this.ws.onmessage = evt => {
      const { data } = evt;
      this.liveList.push({
        text: data,
        score: this.liveList[this.liveList.length - 1]?.score || '00:00'
      });
    }
    this.ws.onclose = function() {
      console.log('Connection closed');
    }
  }
}
</script>

<style scoped>
.live-box {
  border: 1px solid #dedede;
  border-radius: 50px;
  height: 100%;
  box-sizing: border-box;
  justify-content: space-between;
  flex-direction: column;
}

.content {
  border-left: 1px solid #dedede;
  margin: 50px 20px 30px;
  overflow-y: auto;
  overflow-x: hidden;
  height: calc(100% - 60px);
}

.live-item {
  padding-left: 10px;
  display: flex;
  justify-content: space-between;
}

.live-item:not(:last-child) {
  margin-bottom: 30px;
}

.input-bar {
  text-align: center;
  margin: 10px 0;
}

input {
  border: 1px solid #42b983;
  border-radius: 20px;
  padding: 10px;
  margin-right: 10px;
  outline: none;
  font-size: 16px;
  color: #2c3e50;
  width: 300px;
}

button {
  background-color: #42b983;
  color: white;
  cursor: pointer;
  padding: 10px;
  outline: none;
  border: none;
  border-radius: 20px;
  width: 85px;
}
</style>