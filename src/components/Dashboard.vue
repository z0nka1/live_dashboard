<template>
  <div>
    <section class="flex">
      <div class="flex section-title">技术统计</div>
      <div class="flex item-box">
        <div class="commom-item">二分球</div>
        <div class="commom-item">三分球</div>
        <div class="commom-item">篮板球</div>
        <div class="commom-item">助攻</div>
        <div class="commom-item">抢断</div>
        <div class="commom-item">封盖</div>
      </div>
    </section>
    <section class="flex">
      <div class="flex section-title">犯规</div>
      <div class="flex item-box">
        <div class="commom-item">打手</div>
        <div class="commom-item">拉人</div>
        <div class="commom-item">带球撞人</div>
      </div>
    </section>
    <section class="flex">
      <div class="flex section-title">违例</div>
      <div class="flex item-box">
        <div class="commom-item">脚踢球</div>
        <div class="commom-item">二运</div>
      </div>
    </section>
    <section class="flex">
      <div class="flex section-title">暂停</div>
      <div class="flex item-box">
        <div class="commom-item">请求暂停</div>
      </div>
    </section>
    <section class="flex">
      <div class="flex section-title">人员</div>
      <div class="flex item-box">
        <div class="commom-item" v-for="player of players" :key="player">{{ player }}</div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'Dashboard',
  data() {
    return {
      players: ['詹姆斯', '戴维斯', '隆多', '霍华德']
    }
  }
}
</script>

<style scoped>
section {
  border: 1px solid #dedede;
  margin-bottom: -1px;
}

.section-title {
  border-right: 1px solid #dedede;
  flex: 0 0 100px;
  font-size: 16px;
  font-weight: 600;
  justify-content: center;
  align-items: center;
}

.item-box {
  padding: 20px 20px 10px;
  align-items: center;
  flex-wrap: wrap;
}

.commom-item {
  padding: 8px 12px;
  border-radius: 20px;
  cursor: pointer;
  background: #42b983;
  color: white;
  min-width: 72px;
  text-align: center;
  margin-bottom: 8px;
}

.commom-item:not(:last-child) {
  margin-right: 10px;
}
</style>