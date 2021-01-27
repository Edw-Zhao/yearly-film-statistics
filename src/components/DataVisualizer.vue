/* eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /*
eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /*
eslint-disable no-unused-components */ /* eslint-disable no-unused-components */
/* eslint-disable no-unused-components */ /* eslint-disable no-unused-components
*/
<template>
  <div class="component-wrapper">
    <h1 class="header">Genre Data</h1>
    <div class="genre-chart">
      <GenreChart
        v-if="passdata"
        v-bind:genreArray="genreArray"
        v-bind:filmdata="filmdata"
        :height="500"
      />
      <p class="note">Hover over pie segment for genre and the movie count.</p>
    </div>
    <div class="legend-wrapper">
      <div class="legend">
        <div class="chart-label">
          Genre:
        </div>
        <div class="chart-label">
          # of Movies:
        </div>
        <div class="chart-label">
          % of Movies:
        </div>
        <template v-for="n in 9">
          <div
            class="genre-label"
            :key="n"
            v-bind:style="[
              n == 9 ? { 'border-bottom': 'dashed 1px white' } : null,
            ]"
          >
            <div v-bind:style="genreColorsArray[n - 1]" class="circle" />
            <p style="text-indent: 5px">
              {{
                n - 1 === 0
                  ? "Action"
                  : n - 1 === 1
                  ? "Adventure"
                  : n - 1 === 2
                  ? "Animation"
                  : n - 1 === 3
                  ? "Comedy"
                  : n - 1 === 4
                  ? "Crime"
                  : n - 1 === 5
                  ? "Documentary"
                  : n - 1 === 6
                  ? "Drama"
                  : n - 1 === 7
                  ? "Family"
                  : "Fantasy"
              }}
            </p>
          </div>
          <div
            class="genre-label"
            :key="n + 50"
            v-bind:style="[
              n === 9 ? { 'border-bottom': 'dashed 1px white' } : null,
            ]"
          >
            {{ genreArray[n - 1] }}
          </div>
          <div
            class="genre-label"
            :key="n + 100"
            v-bind:style="[
              n == 9 ? { 'border-bottom': 'dashed 1px white' } : null,
            ]"
          >
            {{ Math.round((genreArray[n - 1] / resultsQuan) * 10000) / 100 }}%
          </div>
        </template>
      </div>
      <div class="legend">
        <template v-for="n in 10">
          <div
            class="genre-label"
            :key="n"
            v-bind:style="[
              n === 1 ? { 'border-top': 'dashed 1px white' } : null,
            ]"
          >
            <div v-bind:style="genreColorsArray[n + 8]" class="circle" />
            <p style="text-indent: 5px">
              {{
                n - 1 === 0
                  ? "History"
                  : n - 1 === 1
                  ? "Horror"
                  : n - 1 === 2
                  ? "Music"
                  : n - 1 === 3
                  ? "Mystery"
                  : n - 1 === 4
                  ? "Romance"
                  : n - 1 === 5
                  ? "Science Fiction"
                  : n - 1 === 6
                  ? "TV Movie"
                  : n - 1 === 7
                  ? "Thriller"
                  : n - 1 === 8
                  ? "War"
                  : "Western"
              }}
            </p>
          </div>
          <div
            class="genre-label"
            :key="n + 150"
            v-bind:style="[
              n === 1 ? { 'border-top': 'dashed 1px white' } : null,
            ]"
          >
            {{ genreArray[n + 8] }}
          </div>
          <div
            class="genre-label"
            :key="n + 200"
            v-bind:style="[
              n === 1 ? { 'border-top': 'dashed 1px white' } : null,
            ]"
          >
            {{ Math.round((genreArray[n + 8] / resultsQuan) * 10000) / 100 }}%
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
import GenreChart from "./GenreChart.vue";

export default {
  name: "DataVisualizer",
  props: ["filmdata"],
  components: { GenreChart },
  data() {
    return {
      passdata: false,
      genreArray: [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
      genreColorsArray: [
        "background-color: #e6194B",
        "background-color: #3cb44b",
        "background-color: #4363d8",
        "background-color: #ffe119",
        "background-color: #a9a9a9",
        "background-color: #ffd8b1",
        "background-color: #f58231",
        "background-color: #dcbeff",
        "background-color: #000075",
        "background-color: #fffac8",
        "background-color: #000000",
        "background-color: #bfef45",
        "background-color: #a9a9a9",
        "background-color: #fabed4",
        "background-color: #911eb4",
        "background-color: #ffffff",
        "background-color: #42d4f4",
        "background-color: #FF0000",
        "background-color: #9A6324",
        "background-color: #e6194B",
      ],
      resultsQuan: 0,
      zeroGenreQuan: 0,
      oneGenreQuan: 0,
      twoGenreQuan: 0,
      threeGenreQuan: 0,
      fourGenreQuan: 0,
      fiveGenreQuan: 0,
      sixGenreQuan: 0,
      genreCombinations: 0,
      comboList: {},
    };
  },
  mounted() {
    for (let i = 0; i < this.filmdata.length; i++) {
      this.filmdata[i].filter((film) => {
        this.resultsQuan++;
        if (film.genre_ids.length === 0) {
          this.zeroGenreQuan++;
        }
        if (film.genre_ids.length === 1) {
          this.oneGenreQuan++;
        }
        if (film.genre_ids.length === 2) {
          this.twoGenreQuan++;
        }
        if (film.genre_ids.length === 3) {
          this.threeGenreQuan++;
        }
        if (film.genre_ids.length === 4) {
          this.fourGenreQuan++;
        }
        if (film.genre_ids.length === 5) {
          this.fiveGenreQuan++;
        }
        if (film.genre_ids.length === 6) {
          this.sixGenreQuan++;
        }

        film.genre_ids.forEach((genreids) => {
          if (genreids === 28) {
            this.genreArray[0]++;
          }
          if (genreids === 12) {
            this.genreArray[1]++;
          }
          if (genreids === 16) {
            this.genreArray[2]++;
          }
          if (genreids === 35) {
            this.genreArray[3]++;
          }
          if (genreids === 80) {
            this.genreArray[4]++;
          }
          if (genreids === 99) {
            this.genreArray[5]++;
          }
          if (genreids === 18) {
            this.genreArray[6]++;
          }
          if (genreids === 10751) {
            this.genreArray[7]++;
          }
          if (genreids === 14) {
            this.genreArray[8]++;
          }
          if (genreids === 36) {
            this.genreArray[9]++;
          }
          if (genreids === 27) {
            this.genreArray[10]++;
          }
          if (genreids === 10402) {
            this.genreArray[11]++;
          }
          if (genreids === 9648) {
            this.genreArray[12]++;
          }
          if (genreids === 10749) {
            this.genreArray[13]++;
          }
          if (genreids === 878) {
            this.genreArray[14]++;
          }
          if (genreids === 10770) {
            this.genreArray[15]++;
          }
          if (genreids === 53) {
            this.genreArray[16]++;
          }
          if (genreids === 10752) {
            this.genreArray[17]++;
          }
          if (genreids === 37) {
            this.genreArray[18]++;
          }
        });
      });
    }
    console.log(this.resultsQuan);
    this.passdata = true;
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.component-wrapper {
  padding-top: 40px;
  padding-bottom: 40px;
  width: 100%;
  background-image: linear-gradient(rgb(148, 148, 148), rgb(36, 36, 36));
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.genre-chart {
  padding-top: 40px;
  width: 100%;
  padding-bottom: 20px;
}

.legend-wrapper {
  display: flex;
  width: 100%;
  justify-content: space-around;
  max-width: 1000px;
  margin-top: 20px;
}

.legend {
  display: grid;
  grid-auto-flow: row;
  grid-template-columns: 33.333% 33.333% 33.333%;
  width: 48%;
}

.chart-label {
  border: solid 1px black;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #c40a2f;
  color: white;
  font-weight: bold;
  line-height: 30px;
  font-size: 18px;
}

.genre-label {
  border: solid 1px rgb(255, 255, 0);
  display: flex;
  align-items: center;
  text-indent: 5px;
  text-align: center;
  justify-content: center;
  font-weight: bold;
  color: white;
  height: 30px;
  border-style: groove;
}

.circle {
  height: 10px;
  width: 10px;
  border-radius: 50%;
}

.white-dash-line-top {
  border-top: "dashed 1px white";
}

.white-dash-line-bottom {
  border-bottom: "dashed 1px white";
}

@media only screen and (max-width: 600px) {
  .legend-wrapper {
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .legend {
    width: 96%;
    font-size: 14px;
  }
  .genre-chart {
    padding-top: 0px;
    width: 100%;
    padding-bottom: 0px;
  }
}
</style>
