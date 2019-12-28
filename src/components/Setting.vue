<template>
  <div class="setting">
    <h1>请设置抽奖池</h1>
    <h2>一行一个</h2>
    <div class="field">
      <div class="control">
        <textarea class="textarea" v-model="numbers" />
      </div>
    </div>
    <div class="field is-grouped">
      <div class="control">
        <button class="button is-primary" @click="save">保存</button>
      </div>
      <div class="control">
        <button class="button" @click="clear">清空抽奖历史</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      numbers: ''
    }
  },
  methods: {
    save () {
      localStorage.setItem('numbers', this.numbers)
      alert('已保存')
    },
    clear () {
      localStorage.setItem('history', '')
      alert('已清空')
    }
  },
  mounted () {
    this.numbers = localStorage.getItem('numbers')
  }
}
</script>

<style scoped>
h1 {
  font-size: 30px;
  margin-bottom: 6px;
}

h2 {
  font-size: 20px;
  margin-bottom: 10px;
}

.setting {
  text-align: left;
  width: 50%;
}

.textarea {
  height: 300px;
}
</style>
