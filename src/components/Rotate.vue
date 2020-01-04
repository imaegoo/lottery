<template>
  <div class="rotate">
    <div class="arrow">
      <img class="wheel"
          src="../assets/wheel.png"
          :style="{transform: `rotate(${currentAngle}deg)`}" />
      <div class="pointer" @click="startArrow"></div>
    </div>
    <div class="text" v-if="currentAward" v-html="currentAward"></div>
  </div>
</template>

<script>
const awards = [
  '侯校长发6个6.66元的红包', // 20%
  '阳春三月，遇见美好，带薪休息一天<br>（马校、张校代课）', // 16%
  '黄书记请喝奶茶', // 16%
  '阳春三月，遇见美好，带薪休息半天<br>（樊校代课）', // 16%
  '我和电影有个约会', // 16%
  '2020鼠你有福' // 16%
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
      if (randomNum < 0.2) {
        return 0
      } else if (randomNum < 0.36) {
        return 1
      } else if (randomNum < 0.52) {
        return 2
      } else if (randomNum < 0.68) {
        return 3
      } else if (randomNum < 0.84) {
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
