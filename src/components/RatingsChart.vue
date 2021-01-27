/* eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /*
eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /*
eslint-disable no-unused-components */ /* eslint-disable no-unused-components */
/* eslint-disable no-unused-components */ /* eslint-disable no-unused-components
*/

<script>
import { Line } from "vue-chartjs";

export default {
  name: "DataVisualizer",
  props: ["ratingsArray"],
  extends: Line,
  data() {
    return { ratingsAvgArray: [] };
  },
  mounted() {
    this.ratingsArray.forEach((ratingMonth) => {
      let count = 0;
      let sum = ratingMonth.reduce((a, b) => a + b, 0);
      let avg = sum / ratingMonth.filter((value) => value > 0).length;
      this.ratingsAvgArray.push(Math.round(avg * 10) / 100);
    });
    this.renderChart(
      {
        labels: [
          "January",
          "February",
          "March",
          "April",
          "May",
          "June",
          "July",
          "August",
          "September",
          "October",
          "November",
          "December",
        ],
        datasets: [
          {
            backgroundColor: "yellow",
            data: this.ratingsAvgArray,
            fill: false,
            label: "Average Rating Per Month",
            fontColor: "white",
            borderColor: "#c40a2f",
            pointRadius: 5,
          },
        ],
      },
      {
        responsive: true,
        maintainAspectRatio: false,
        legend: {
          labels: {
            fontColor: "black",
            fontSize: 16,
          },
        },
        scales: {
          yAxes: [
            {
              ticks: {
                beginAtZero: false,
                fontColor: "black",
              },
              gridLines: {
                display: true,
                lineWidth: 1,
                zeroLineColor: "white",
              },
            },
          ],
          xAxes: [
            {
              ticks: {
                beginAtZero: false,
                fontColor: "black",
              },
              gridLines: {
                display: true,
                lineWidth: 1,
              },
            },
          ],
        },
      }
    );
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
