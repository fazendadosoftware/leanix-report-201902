<template>
  <div id="app">
    <div class="chart-outer-container">
      <div class="chart-inner-container">
        <line-chart/>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: { Chart, FactsheetCard },
  mounted () {
    this.fillData()
    this.$lx.init()
      .then(setup => {
        this.$lx.ready({})
      })
  }
}
</script>

<style lang="stylus">
  @import './stylus/main'

  #app
    display flex
    flex-flow column
    justify-content center
    align-items center
    height calc(100vh - 20px)
    background
</style>
