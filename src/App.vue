<template>
  <div id="app">
    <div>
      <Header />
    </div>
    <div class="flex content">
      <div id="live-box">
        <LiveBox :ws="ws" />
      </div>
      <div id="dashboard">
        <div>
          <Dashboard />
        </div>
        <div>
          <InputBox :ws="ws" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Dashboard from "./components/Dashboard.vue";
import LiveBox from "./components/LiveBox.vue";
import Header from "./components/Header.vue";
import InputBox from "./components/InputBox.vue";

export default {
  name: "App",
  components: {
    Dashboard,
    LiveBox,
    Header,
    InputBox
  },
  data() {
    return {
      ws: new WebSocket("wss://echo.websocket.org")
    }
  },
  mounted() {
    this.ws.onopen = function() {
      console.log('Connection open...');
    }
    this.ws.onclose = function() {
      console.log('Connection closed');
    }
  },
  destroyed() {
    this.ws.close();
  }
};
</script>

<style>
* {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#dashboard {
  flex: 1 1 500px;
}

#dashboard > div:nth-child(1) {
  margin-bottom: 20px;
}

#live-box {
  flex: 0 0 600px;
  padding: 0 20px;
}

.flex {
  display: flex;
}

.content {
  height: calc(100% - 150px);
}
</style>
