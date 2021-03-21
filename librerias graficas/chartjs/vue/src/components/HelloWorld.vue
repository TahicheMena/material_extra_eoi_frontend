<template>
  <div>
    <canvas id="chart" width="600px" height="600px"></canvas>
  </div>
</template>

<script>
import Chart from "chart.js";
import axios from "axios";

export default {
  name: "HelloWorld",
  data() {
    return {
      myChart: {},
    };
  },
  mounted() {
    axios
      .get(
        "https://tahichemena.github.io/curso_frontend_2019/graficas/data/stats_01.json"
      )
      .then((response) => this.drawChart(response.data));
  },
  methods: {
    drawChart(anxietyMoments) {
      let momentos = [];
      let ansiedades = [];
      anxietyMoments.data.forEach((anxietyMoment) => {
        momentos.push(anxietyMoment.momento);
        ansiedades.push(anxietyMoment.ansiedad);
      });
      Chart.defaults.global.defaultFontSize = 15;
      this.myChart = new Chart(document.getElementById("chart"), {
        type: "bar",
        data: {
          labels: momentos,
          datasets: [
            {
              label: "Ansiedad",
              data: ansiedades,
              backgroundColor: function (context) {
                // Scriptable
                var index = context.dataIndex; // Indexable
                var value = context.dataset.data[index];
                var alpha = value / 15;
                return "rgb(255,150,0," + alpha + ")";
              },
              borderColor: "rgba(255,150,0,0.75)",
              borderWidth: 1,
            },
          ],
        },
        options: {
          scales: {
            yAxes: [
              {
                scaleLabel: {
                  display: true,
                  labelString: "Cantidad de ansiedad",
                },
                ticks: {
                  beginAtZero: true,
                },
              },
            ],
          },
          title: {
            display: true,
            text: anxietyMoments.title,
          },
        },
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
