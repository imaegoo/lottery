<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Setting />
  </div>
</template>

<script>
import Setting from './components/Setting.vue'

export default {
  name: 'app',
  components: {
    Setting
  },
  data () {
    return {
      page: ''
    }
  },
  mounted () {
    this.page = 'setting'
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
