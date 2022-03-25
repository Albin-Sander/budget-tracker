<template>
  <DoughnutChart :chartData="testData" :options="options" />
</template>

<script>
import { defineComponent } from "@vue/runtime-core";
import { DoughnutChart, useDoughnutChart } from "vue-chart-3";
import { Chart, registerables } from "chart.js";
import { computed, ref } from "vue";
import ChartJSPluginDatalabels from "chartjs-plugin-datalabels";

Chart.register(...registerables);
Chart.register(ChartJSPluginDatalabels);
export default defineComponent({
  name: "Chart",
  components: { DoughnutChart },

  props: {
    prices: Array,
    categories: Array,
  },

  setup(props) {
    const testData = computed(() => ({
      labels: props.categories,
      datasets: [
        {
          data: props.prices,
          backgroundColor: [
            "#77CEFF",
            "#faedcc",
            "#deecdc",
            "#e6deed",
            "#A5C8ED",
          ],
          plugins: {
            datalabels: {
              color: "white",
              textAlign: "center",
              font: {
                weight: "bold",
                size: 16,
              },
            },
          },
        },
      ],
    }));

    const options = ref({
      responsive: true,
      plugins: {
        legend: {
          position: "top",
        },
        title: {
          display: true,
          text: "Spent this month",
        },
      },
    });

    const { doughnutChartProps, doughnutChartRef } = useDoughnutChart({
      chartData: testData,
    });

    return {
      doughnutChartProps,
      doughnutChartRef,
      testData,
      options,
    };
  },
});
</script>

<style></style>
