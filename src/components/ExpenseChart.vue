<template>
  <canvas style="width: 60%;" ref="chartCanvas"></canvas>
</template>

<script setup>
import { onMounted, ref, watch } from 'vue'
import Chart from 'chart.js/auto'
const props = defineProps(['transactions'])
const chartCanvas = ref(null)
let chartInstance = null

const renderChart = () => {
  if (chartInstance) chartInstance.destroy()
  const data = {}
  props.transactions.filter(t => t.type === 'خرج').forEach(t => {
    data[t.category] = (data[t.category] || 0) + t.amount
  })
  chartInstance = new Chart(chartCanvas.value, {
    type: 'pie',
    data: {
      labels: Object.keys(data),
      datasets: [{ data: Object.values(data), backgroundColor: ['#f44336', '#2196f3', '#4caf50', '#ff9800', '#9c27b0'] }]
    }
  })
}

onMounted(renderChart)
watch(() => props.transactions, renderChart, { deep: true })
</script>
