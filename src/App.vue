<template>
  <div id="app">
    <div class="chart-container">
      <chart :chart-data="chartData" :options="chartOptions"/>
    </div>
  </div>
</template>

<script>
import Chart from './components/Chart'

export default {
  name: 'App',
  components: {
    Chart
  },
  data () {
    return {
      rawData: [],
      datacollection: null,
      chartData: {
        labels: ['2018', '2019', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
        datasets: [
          {
            label: 'Gesamt',
            backgroundColor: 'red',
            data: [40, 20, 12, 39, 10, 40, 39, 80, 40, 20, 12, 11]
          },
          {
            label: 'Projekt',
            backgroundColor: 'green',
            data: [40, 20, 12, 39, 10, 40, 39, 80, 40, 20, 12, 11]
          },
          {
            label: 'Betrieb',
            backgroundColor: 'blue',
            data: [40, 20, 12, 39, 10, 40, 39, 80, 40, 20, 12, 11]
          }
        ]
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false
      }
    }
  },
  methods: {
    getRandomInt () {
      return Math.floor(Math.random() * (50 - 5 + 1)) + 5
    },
    fillData () {
      this.datacollection = {
        labels: [this.getRandomInt(), this.getRandomInt()],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979',
            data: [this.getRandomInt(), this.getRandomInt()]
          }, {
            label: 'Data One',
            backgroundColor: '#f87979',
            data: [this.getRandomInt(), this.getRandomInt()]
          }
        ]
      }
    },
    getDataset () {
      const years = [2017, 2018, 2019, 2020, 2021, 2022, 2023]
      const costTypes = ['project', 'op', 'total']
      const costFragment = years
        .map(year => `y${year}`).map(yearPrefix => costTypes.map(costType => `${yearPrefix}${costType}`))
        .reduce((accumulator, yearPrefix) => Array.from([...accumulator, ...yearPrefix.map(year => `${year}Costs`)]), [])
      const query = `{op:allFactSheets(factSheetType: Application){edges{node{...on Application{id name ${costFragment}}}}}}`
      return this.$lx.executeGraphQL(query)
        .then(res => res.op.edges
          .map(edge => edge.node)
          .reduce((accumulator, node) => {
            const keyedByYear = years
              .map(year => Object
                .keys(node)
                .filter(key => key.indexOf(year) > -1)
                .reduce((accumulator, key) => {
                  accumulator[key.replace(`y${year}`, '')] = node[key]
                  return accumulator
                }, { id: node.id, name: node.name, year })
              )
            return Array.from([...accumulator, ...keyedByYear])
          }, [])
        )
    }
  },
  mounted () {
    this.fillData()
    this.$lx.init()
      .then(setup => {
        this.$lx.ready({})
      })
    this.getDataset()
      .then(dataset => { this.rawData = dataset })
  }
}
</script>

<style lang="stylus" scoped>
  @import './stylus/main'

  #app
    display flex
    flex-flow column
    justify-content center
    align-items center
    height calc(100vh - 20px)

</style>
