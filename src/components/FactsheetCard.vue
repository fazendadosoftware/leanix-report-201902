<template>
  <div class="card shadow">
    <line-chart :chart-data="chartData" :options="chartOptions" />
    <div class="action-row">
      <span class="btn clickable">
        <font-awesome-icon icon="file-download" size="lg" /> Export
      </span>
    </div>
  </div>
</template>

<script>
// export ot pdf
// https://github.com/apertureless/vue-chartjs/issues/89
import LineChart from '@/components/LineChart'
export default {
  name: 'FactsheetCard',
  components: { LineChart },
  data () {
    return {
      // https://www.chartjs.org/docs/latest/charts/line.html
      chartData: {
        labels: ['2017', '2018', '2019', '2020', '2021', '2022', '2023'],
        datasets: [
          {
            label: 'Operating Costs',
            fill: false,
            backgroundColor: 'transparent',
            borderColor: '#689f38',
            borderWidth: 1,
            pointBackgroundColor: '#689f38',
            data: [40, 39, 10, 40, 39, 80, 40]
          },
          {
            label: 'Project Costs',
            fill: false,
            backgroundColor: 'transparent',
            borderColor: '#004ba0',
            borderWidth: 1,
            pointBackgroundColor: '#004ba0',
            data: [12, 11, 25, 10, 40, 70, 70]
          },
          {
            label: 'Total Costs',
            fill: false,
            backgroundColor: 'transparent',
            borderColor: '#ac0800',
            borderWidth: 1,
            pointBackgroundColor: '#ac0800',
            data: [52, 50, 35, 50, 79, 150, 110]
          }
        ]
      },
      chartOptions: {
        title: {
          display: true,
          position: 'top',
          text: 'Application A',
          fontSize: 14,
          fontStyle: 'bold'
        },
        responsive: true,
        maintainAspectRatio: false,
        tooltips: {
          mode: 'point',
          intersect: false,
          position: 'nearest'
        },
        hover: {
          mode: 'nearest',
          intersect: true
        },
        scales: {
          yAxes: [
            {
              scaleLabel: {
                display: true,
                labelString: 'Cost (k€)',
                fontStyle: 'bold'
              }
            }
          ]
        },
        legend: {
          display: false,
          position: 'bottom',
          labels: {
            usePointStyle: true
          }
        },
        elements: {
          point: {
            radius: 2,
            hitRadius: 10,
            hoverRadius: 5
          }
        }
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
  border-radius 6px
  display flex
  flex-flow column

.action-row
  margin-top 1rem
  display flex
  justify-content flex-end
  padding 0 5px

.btn
  color #333
  cursor pointer
  font-size 12px
  > svg
    padding-right 5px
  &:hover
    text-decoration underline

.shadow
  box-shadow 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24)
  transition all 0.3s cubic-bezier(.25,.8,.25,1)
</style>
