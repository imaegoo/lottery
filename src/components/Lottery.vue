<template>
  <div class="lottery">
    <div class="current">{{ current }}</div>
    <button class="button is-large is-primary" v-if="!timer" @click="start">开始</button>
    <button class="button is-large is-danger" v-if="timer" @click="stop">停</button>
    <table class="table" v-if="history.length > 0">
      <thead>
        <tr>
          <th>轮次</th>
          <th>中奖号码</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in history" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ item }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data () {
    return {
      numbers: [],
      current: '',
      timer: null,
      history: []
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
      this.timer = null
      this.saveHistory()
    },
    refresh () {
      this.current = this.numbers[this.random(0, this.numbers.length - 1)]
    },
    saveHistory () {
      this.history.push(this.current)
      localStorage.setItem('history', JSON.stringify(this.history))
    },
    readNumbers () {
      const numStr = localStorage.getItem("numbers")
      if (numStr) this.numbers = numStr.split('\n').filter((item) => !!item)
      if (this.numbers.length === 0) alert('抽奖池为空')
    },
    readHistory () {
      const history = localStorage.getItem("history")
      if (history) this.history = JSON.parse(history)
    }
  },
  mounted () {
    this.readNumbers()
    this.readHistory()
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

.table {
  position: fixed;
  left: 20px;
  bottom: 20px;
  background-color: transparent;
  color: #ffffff;
}

.table thead td, .table thead th {
  color: #ffffff;
}
</style>
