<template>
  <div class="flex live-box">
    <div class="content">
      <div class="live-item" v-for="(live, idx) in liveList" :key="idx + live.text">
        <span>{{ live.text }}</span>
        <span>{{ live.score }}</span>
      </div>
      <div class="live-item" v-if="!liveList.length">比赛尚未开始！</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LiveBox',
  props: ['ws'],
  data() {
    return {
      liveList: []
    }
  },
  mounted() {
    this.ws.onmessage = evt => {
      const { data } = evt;
      this.liveList.push({
        text: data,
        score: this.liveList[this.liveList.length - 1]?.score || '00:00'
      });
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
</style>