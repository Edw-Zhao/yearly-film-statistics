/* eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /*
eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /*
eslint-disable no-unused-components */ /* eslint-disable no-unused-components */
/* eslint-disable no-unused-components */ /* eslint-disable no-unused-components
*/

<script>
import { Pie } from "vue-chartjs";

export default {
  name: "DataVisualizer",
  props: ["genreArray", "resultsQuan"],
  extends: Pie,
  mounted() {
    this.renderChart(
      {
        labels: [
          `Action `, //${Math.round((100 * this.genreArray[0]) / this.resultsQuan)}
          "Adventure",
          "Animation",
          "Comedy",
          "Crime",
          "Documentary",
          "Drama",
          "Family",
          "Fantasy",
          "History",
          "Horror",
          "Music",
          "Mystery",
          "Romance",
          "Science Fiction",
          "TV Movie",
          "Thriller",
          "War",
          "Western",
        ],
        datasets: [
          {
            backgroundColor: [
              "#f87979",
              "#3cb44b",
              "#4363d8",
              "#ffe119",
              "#a9a9a9",
              "#ffd8b1",
              "#f58231",
              "#dcbeff",
              "#000075",
              "#fffac8",
              "#000000",
              "#bfef45",
              "#a9a9a9",
              "#fabed4",
              "#911eb4",
              "#ffffff",
              "#42d4f4",
              "#FF0000",
              "#9A6324",
            ],
            data: this.genreArray,
          },
        ],
      },
      {
        responsive: true,
        maintainAspectRatio: false,
        showLabels: false,
        legend: {
          display: false,
        },
      }
    );
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
