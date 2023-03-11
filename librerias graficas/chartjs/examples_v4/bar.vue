<template>
    <main class="container">
      <div>
        <!-- Canvas dónde se dibuja la gráfica -->
        <canvas ref="chart" width="1000" height="500">Su navegador no puede visualizar la gráfica</canvas>
      </div>
    </main>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue';
  import Chart from 'chart.js/auto';
  
  export default {
    setup() {
      const chartRef = ref(null);
  
      onMounted(() => {
        Chart.defaults.font.size = 18;
        const ctx = chartRef.value.getContext('2d');
        // Bar chart
        new Chart(ctx, {
          type: 'bar',
          data: {
            labels: ['Videojuegos', 'Netflix', 'Comer pizza', 'Comer sano', 'Dormir'],
            datasets: [
              {
                label: 'Mis prioridades',
                data: [10, 9, 7, 3, 2],
                backgroundColor: [
                  'rgba(255, 99, 132, 0.2)',
                  'rgba(255, 159, 64, 0.2)',
                  'rgba(255, 205, 86, 0.2)',
                  'rgba(75, 192, 192, 0.2)',
                  'rgba(54, 162, 235, 0.2)',
                ],
                borderColor: [
                  'rgb(255, 99, 132)',
                  'rgb(255, 159, 64)',
                  'rgb(255, 205, 86)',
                  'rgb(75, 192, 192)',
                  'rgb(54, 162, 235)',
                ],
                borderWidth: 1,
              },
            ],
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
          },
        });
      });
  
      return { chartRef };
    },
  };
  </script>
  