<template>
  <div class="header">
    <div class="title">洛杉矶湖人 VS 迈阿密热火</div>
    <div>第1节 09:56</div>
    <div class="score">12 : 13</div>
  </div>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<style scoped>
.header {
  text-align: center;
  padding: 20px;
}

.header > div {
  margin-bottom: 6px;
}

.title {
  font-size: 18px;
  font-weight: 600;
}

.score {
  font-size: 18px;
  font-weight: 600;
}
</style>