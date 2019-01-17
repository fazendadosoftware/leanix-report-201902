<template>
  <div id="app">
    <factsheet-card />
  </div>
</template>

<script>
import FactsheetCard from '@/components/FactsheetCard'

export default {
  name: 'App',
  components: { FactsheetCard },
  mounted () {
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
    justify-content center
    align-items center
    height calc(100vh - 20px)
</style>
