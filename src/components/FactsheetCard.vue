<template>
  <div class="card shadow">
    <div class="title">Title</div>
    <div class="title">Chart</div>
    <line-chart :chart-data="chartData" :options="chartOptions"/>
  </div>
</template>

<script>
import LineChart from '@/components/LineChart'
export default {
  name: 'FactsheetCard',
  components: { LineChart },
  data () {
    return {
      chartData: {
        labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979',
            data: [40, 39, 10, 40, 39, 80, 40]
          }
        ]
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false
      }
    }
  }
}
</script>

<style lang="stylus" scoped>

.card
  padding 1rem
  background white
  color grey
  cursor default
  border-radius 3px
  display flex
  flex-flow column

.shadow
  box-shadow 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24)
  transition all 0.3s cubic-bezier(.25,.8,.25,1)
  &:hover
    box-shadow 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22)
</style>
