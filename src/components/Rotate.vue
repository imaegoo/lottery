<template>
  <div class="rotate">
    <div class="arrow">
      <img class="wheel"
          src="../assets/wheel.png"
          :style="{transform: `rotate(${currentAngle}deg)`}" />
      <div class="pointer" @click="startArrow"></div>
    </div>
    <div class="text" v-if="currentAward">{{ currentAward }}</div>
  </div>
</template>

<script>
const awards = [
  '侯校长发红包', // 30%
  '工作日不扣工资，休息一天', // 10%
  '与黄书记共进晚餐', // 10%
  '工作日不扣工资，休息半天', // 10%
  '教研组最美（最帅）的人请喝奶茶', // 15%
  '跟校长们合张影' // 25%
]

export default {
  props: {
    msg: String
  },
  data() {
    return {
      currentAngle: 0,
      times: 0,
      currentAward: '等待抽奖'
    }
  },
  methods: {
    startArrow() {
      if (this.currentAward === '正在抽奖') return
      let award = this.getAward()
      this.getAngle(award)
      this.setCurrentAward(award)
    },
    getAward() {
      let randomNum = Math.random()
      if (randomNum < 0.3) {
        return 0
      } else if (randomNum < 0.4) {
        return 1
      } else if (randomNum < 0.5) {
        return 2
      } else if (randomNum < 0.6) {
        return 3
      } else if (randomNum < 0.75) {
        return 4
      } else if (randomNum <= 1) {
        return 5
      }
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
</style>
