<template>
  <div id="app">
    <div class="background"></div>
    <nav class="nav">
      <div class="nav-item"
          v-for="component in components"
          :key="component.path"
          @click="page = component.path">
        {{ component.name }}
      </div>
    </nav>
    <div class="component">
      <Setting v-if="page === 'Setting'" />
      <Lottery v-if="page === 'Lottery'" />
    </div>
  </div>
</template>

<script>
import Setting from './components/Setting.vue'
import Lottery from './components/Lottery.vue'

const Components = [
  { path: 'Lottery', name: '抽奖' },
  { path: 'Setting', name: '设置' }
]

export default {
  name: 'app',
  components: {
    Setting,
    Lottery
  },
  data () {
    return {
      page: ''
    }
  },
  computed: {
    components () {
      return Components
    }
  },
  mounted () {
    this.page = 'Lottery'
  }
}
</script>

<style>
body {
  margin: 0;
}

.background {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-image: url('./assets/bg-1.png');
}

#app {
  font-family: 'Microsoft YaHei', 'SimHei';
  text-align: center;
  color: #ffffff;
}

.nav {
  background-color: transparent;
  position: fixed;
  top: 0;
  right: 10px;
  display: flex;
}

.nav .nav-item {
  cursor: pointer;
  width: 4rem;
  height: 3.25rem;
  line-height: 3.25rem;
  color: #ffffff;
}

.nav .nav-item:hover {
  background-color: rgba(255, 255, 255, 0.5);
}

.component {
  position: fixed;
  top: 3.25rem;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: auto;
}

::selection {
  background-color: rgba(255, 255, 0, 0.5);
}
::-moz-selection {
  background-color: rgba(255, 255, 0, 0.5);
}
</style>
