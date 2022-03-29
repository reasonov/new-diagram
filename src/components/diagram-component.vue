<template>
  <DoughnutChart :chartData="testData" :options="chartOptions" :width="260" :height="260" />

  <graph-circle />
</template>

<script>
import { DoughnutChart } from 'vue-chart-3';
import { Chart, registerables } from "chart.js";
import graphCircle from "@/components/graph-circle";

Chart.register(...registerables);

export default {
  name: "App",
  components: {
    DoughnutChart,
    graphCircle
  },
  setup() {
    const testData = {
      datasets: [
        {
          data: [41, 39, 13, 7],
          backgroundColor: ['#FFC549', '#4ADDBC', '#CDCDCD', '#575C62'],
        },
      ],
    }

    const chartOptions = {
      borderWidth: 1,
      cutout: '90%'
    }

    return { testData, chartOptions }

  }
};
</script>