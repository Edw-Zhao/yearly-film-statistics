/* eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /*
eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /*
eslint-disable no-unused-components */ /* eslint-disable no-unused-components */
/* eslint-disable no-unused-components */ /* eslint-disable no-unused-components
*/

<script>
import { Bar } from "vue-chartjs";

export default {
  name: "DataVisualizer",
  props: ["dateData"],
  extends: Bar,
  data() {
    return {
      dateArray: [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    };
  },
  mounted() {
    this.dateData.forEach((event) => {
      if (new Date(event.date).getMonth() === 0) {
        this.dateArray[0]++;
      }
      if (new Date(event.date).getMonth() === 1) {
        this.dateArray[1]++;
      }
      if (new Date(event.date).getMonth() === 2) {
        this.dateArray[2]++;
      }
      if (new Date(event.date).getMonth() === 3) {
        this.dateArray[3]++;
      }
      if (new Date(event.date).getMonth() === 4) {
        this.dateArray[4]++;
      }
      if (new Date(event.date).getMonth() === 5) {
        this.dateArray[5]++;
      }
      if (new Date(event.date).getMonth() === 6) {
        this.dateArray[6]++;
      }
      if (new Date(event.date).getMonth() === 7) {
        this.dateArray[7]++;
      }
      if (new Date(event.date).getMonth() === 8) {
        this.dateArray[8]++;
      }
      if (new Date(event.date).getMonth() === 9) {
        this.dateArray[9]++;
      }
      if (new Date(event.date).getMonth() === 10) {
        this.dateArray[10]++;
      }
      if (new Date(event.date).getMonth() === 11) {
        this.dateArray[11]++;
      }
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
            backgroundColor: "#c40a2f",
            data: this.dateArray,
            label: "# Theatrical Releases Per Month",
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
