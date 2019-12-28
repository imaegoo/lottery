<template>
  <div>
    <h1>请设置抽奖池</h1>
    <h2>一行一个</h2>
    <textarea v-model="numbers" />
  </div>
</template>

<script>
export default {
  data () {
    return {
      numbers: ''
    }
  }
}
</script>
