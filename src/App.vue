<template>
  <div id="app">
    <div class="background"></div>
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-menu">
        <div class="navbar-end">
          <a class="navbar-item"
              v-for="component in components"
              :key="component.path"
              @click="page = component.path">
            {{ component.name }}
          </a>
        </div>
      </div>
    </nav>
    <div class="component">
      <Setting v-if="page === 'Setting'" />
      <Call v-if="page === 'Call'" />
      <Lottery v-if="page === 'Lottery'" />
    </div>
  </div>
</template>

<script>
import Setting from './components/Setting.vue'
import Call from './components/Call.vue'
import Lottery from './components/Lottery.vue'

const Components = [
  { path: 'Lottery', name: '抽奖' },
  { path: 'Call', name: '拨号' },
  { path: 'Setting', name: '设置' }
]

export default {
  name: 'app',
  components: {
    Setting,
    Call,
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

.navbar {
  background-color: transparent;
}

.navbar-end {
  margin-right: 10px;
}

.navbar-item {
  color: #ffffff;
}

a.navbar-item:hover {
  color: #ffffff;
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
  background-color: transparent;
}
::-moz-selection {
  background-color: transparent;
}
</style>
