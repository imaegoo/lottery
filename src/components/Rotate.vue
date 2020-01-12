<template>
  <div class="rotate">
    <div class="arrow">
      <img class="wheel"
          src="../assets/wheel.png"
          :style="{transform: `rotate(${currentAngle}deg)`}" />
      <div class="pointer" @click="startArrow"></div>
    </div>
    <div class="text" v-if="currentAward" v-html="currentAward"></div>
    <div class="histories" v-show="false">
      <span v-for="(history, index) in histories" :key="index">{{ history }}</span>
    </div>
  </div>
</template>

<script>
const awards = [
  '阳春三月遇见美好<br>（带薪休假半天，樊校代课）',
  '我吃牛排要你陪<br>（蔡主任今天陪你去正弘城吃牛排并买单）',
  '我喝奶茶你买单<br>（黄书记请你喝奶茶）',
  '我和电影有个约会<br>（冯校长送你三张电影票）',
  '初夏五月向美而行<br>（带薪休假1天，马校代课）',
  '鲜花送佳人<br>（张校长送你一束鲜花并送你回家）'
]

export default {
  props: {
    msg: String
  },
  data() {
    return {
      currentAngle: 0,
      times: 0,
      currentAward: '等待抽奖<br>',
      histories: []
    }
  },
  methods: {
    startArrow() {
      if (this.currentAward === '正在抽奖<br>') return
      let award = this.getAward()
      this.getAngle(award)
      this.setCurrentAward(award)
    },
    getAward() {
      let randomNum
      if (this.histories.length >= awards.length) {
        randomNum = this.histories.shift()
      } else {
        do {
          randomNum = Math.floor(Math.random() / (1 / awards.length))
        } while (this.histories.some((history) => history === randomNum))
      }
      this.histories.push(randomNum)
      return randomNum
    },
    getAngle(award) {
      this.times++
      let max = (award + 1) * 60
      let min = award * 60
      let angle = parseInt(Math.random() * (max - min + 1) + min, 10)
      this.currentAngle = 360 * (this.times * 7) + angle
    },
    setCurrentAward(award) {
      this.currentAward = '正在抽奖'
      setTimeout(() => {
        this.currentAward = `恭喜中奖：${awards[award]}`
      }, 5000)
    }
  }
}
</script>

<style scoped>
.arrow {
  position: relative;
}
.wheel {
  transition: transform 5s;
}
.pointer {
  background-repeat: no-repeat;
  background-position: center;
  background-image: url('../assets/arrow.png');
  content: '';
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  position: absolute;
}
.text {
  margin-top: 20px;
  font-size: 26px;
  font-weight: bold;
}
.histories {
  position: fixed;
  right: 10px;
  bottom: 10px;
}
</style>
