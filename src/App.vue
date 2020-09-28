<template>
  <div id="app">
    <div>
      <Header />
    </div>
    <div class="flex content">
      <div id="dashboard-1">
        <Dashboard />
      </div>
      <div id="live-box">
        <LiveBox />
      </div>
      <div id="dashboard-2">
        <Dashboard />
      </div>
    </div>
  </div>
</template>

<script>
import Dashboard from "./components/Dashboard.vue";
import LiveBox from "./components/LiveBox.vue";
import Header from "./components/Header.vue";

export default {
  name: "App",
  components: {
    Dashboard,
    LiveBox,
    Header
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#dashboard-1,
#dashboard-2 {
  flex: 1 1 300px;
}

#live-box {
  flex: 0 0 500px;
  padding: 0 20px;
}

.flex {
  display: flex;
}

.content {
  height: calc(100% - 150px);
}
</style>
