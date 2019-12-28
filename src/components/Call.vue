<template>
  <div class="lottery">
    <div class="current">{{ current }}</div>
    <button class="button is-large is-primary" v-if="!timer" @click="start">开始</button>
    <button class="button is-large is-danger" v-if="timer" @click="stop">停</button>
  </div>
</template>

<script>
const HardCodePhone = '15803999090'
const RandomPhones = [
  '13165901716', '18868935415', '13591505879', '13684787147', '15920304651',
  '13761318798', '18658726990', '15042456737', '18817787450', '18699302713',
  '13146819966', '13121864423', '13905513697', '18742418000', '13195726576',
  '18604987878', '15845989709', '13811903168', '15915763334', '18671777020'
]

export default {
  data () {
    return {
      numbers: RandomPhones,
      current: '',
      timer: null
    }
  },
  methods: {
    random (minNum, maxNum) {
      return parseInt(Math.random() * (maxNum - minNum + 1) + minNum)
    },
    start () {
      this.timer = setInterval(this.refresh, 50)
    },
    stop () {
      clearInterval(this.timer)
      this.current = HardCodePhone
      this.timer = null
    },
    refresh () {
      this.current = this.numbers[this.random(0, this.numbers.length - 1)]
    }
  },
  mounted () {
    this.current = this.numbers[0].split('').map(() => '*').join('')
  }
}
</script>

<style scoped>
h1 {
  font-size: 30px;
}

h2 {
  font-size: 20px;
}

.current {
  font-size: 200px;
  margin-bottom: 50px;
}

.button.is-large {
  font-weight: bold;
  width: 100px;
}

.table {
  position: fixed;
  left: 20px;
  bottom: 20px;
}
</style>
