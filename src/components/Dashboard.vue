<template>
  <div>
    <section class="flex">
      <div class="flex section-title">技术统计</div>
      <div class="flex item-box">
        <div
          v-for="(tech, idx) in techList"
          :key="tech.text"
          :class="[{ 'selected': tech.isSelected }, 'commom-item']"
          @click="itemClick(techList, idx)"
        >
          {{ tech.text }}
        </div>
      </div>
    </section>
    <section class="flex">
      <div class="flex section-title">犯规</div>
      <div class="flex item-box">
        <div
          v-for="(foul, idx) in foulList"
          :key="foul.text"
          :class="[{ 'selected': foul.isSelected }, 'commom-item']"
          @click="itemClick(foulList, idx)"
        >
          {{ foul.text }}
        </div>
      </div>
    </section>
    <section class="flex">
      <div class="flex section-title">违例</div>
      <div class="flex item-box">
        <div
          v-for="(offence, idx) in offenceList"
          :key="offence.text"
          :class="[{ 'selected': offence.isSelected }, 'commom-item']"
          @click="itemClick(offenceList, idx)"
        >
          {{ offence.text }}
        </div>
      </div>
    </section>
    <section class="flex">
      <div class="flex section-title">主队</div>
      <div class="flex item-box">
        <div
          v-for="(player, idx) of homeTeam"
          :key="player.text"
          :class="[{ 'selected': player.isSelected }, 'commom-item']"
          @click="itemClick(homeTeam, idx)"
        >
          {{ player.text }}
        </div>
      </div>
    </section>
    <section class="flex">
      <div class="flex section-title">客队</div>
      <div class="flex item-box">
        <div
          v-for="(player, idx) of guestTeam"
          :key="player.text"
          :class="[{ 'selected': player.isSelected }, 'commom-item']"
          @click="itemClick(guestTeam, idx)"
        >
          {{ player.text }}
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import { EventBus } from './../utils/EventBus';
import { defaultTech, defaultFoul, defaultOffence, homeTeam, guestTeam } from './../mock/mockData';

const keys = ['techList', 'foulList', 'offenceList', 'homeTeam', 'guestTeam'];

export default {
  name: "Dashboard",
  data() {
    return {
      techList: [...defaultTech],
      foulList: [...defaultFoul],
      offenceList: [...defaultOffence],
      homeTeam: [...homeTeam],
      guestTeam: [...guestTeam]
    };
  },
  methods: {
    itemClick(list, idx) {
      if (list[idx].isSelected) return;
      list.forEach(item => {
        item.isSelected = false;
      });
      list[idx].isSelected = true;
      EventBus.$emit('itemClick', list[idx].value || list[idx].text);
    },
    refresh() {
      keys.forEach(key => {
        this[key].forEach(item => {
          item.isSelected = false;
        });
      });
    }
  },
  mounted() {
    EventBus.$on('refresh', () => {
      this.refresh();
    })
  }
};
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
  border: 1px solid #42b983;
  min-width: 72px;
  text-align: center;
  margin-bottom: 8px;
}

.commom-item.selected {
  background: #42b983;
  color: white;
}

.commom-item:not(:last-child) {
  margin-right: 10px;
}
</style>