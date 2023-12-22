<template>
  <Bar id="Pokemon-stat-chart" :options="chartOptions" :data="chartData" />
</template>

<script>
import {
  BarElement,
  CategoryScale,
  Chart as ChartJS,
  Legend,
  LinearScale,
  Title,
  Tooltip
} from 'chart.js'
import { Bar } from 'vue-chartjs'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  props: {
    pokemonStats: {
      type: [],
      required: true
    }
  },
  components: { Bar },
  data() {
    return {
      chartData: {
        labels: this.pokemonStats.map((stat) => stat.stat.name),
        datasets: [
          {
            label: 'Pokemon Stats',
            backgroundColor: '#f61c20',
            data: this.pokemonStats.map((stat) => stat.base_stat)
          }
        ]
      },
      chartOptions: {
        responsive: true
      }
    }
  }
}
</script>
