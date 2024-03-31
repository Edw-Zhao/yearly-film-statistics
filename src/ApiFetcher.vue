/* eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars
*/ /* eslint-disable no-unused-components */ /* eslint-disable no-unused-components */ /* eslint-disable no-unused-components */ /*
eslint-disable no-unused-components */

<template>
  <div id="api-fetcher-wrapper">
    <Calendar v-if="gotFilmResults" v-bind:filmdata="filmresults" v-bind:yearInput="yearInput" />
    <DataVisualizer v-if="gotFilmResults" v-bind:filmdata="filmresults" />
    <PopularMovies v-if="gottop10results && gotFilmResults" v-bind:toptendata="top10results" />
  </div>
</template>

<script>
import Calendar from "./components/CalendarData.vue";
import DataVisualizer from "./components/DataVisualizer.vue";
import PopularMovies from "./components/PopularMovies.vue";
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
Vue.use(VueAxios, axios);

export default {
  name: "ApiFetcher",
  props: ["yearInput", "gotFilmResults"],
  components: {
    Calendar,
    DataVisualizer,
    PopularMovies,
  },
  data() {
    return {
      gottop10results: false,
      filmresults: [],
      top10results: {},
    };
  },
  async mounted() {
    let totalPagesCount;

    await axios
      .get(
        `https://api.themoviedb.org/3/discover/movie?api_key=a1b84ce27d6ea9262430dc19dfd4646c&language=en-US&region=US&sort_by=popularity.desc&include_adult=false&include_video=false&year=${this.yearInput}&with_release_type=3&with_original_language=en`
      )
      .then((response) => (totalPagesCount = response.data.total_pages))
      .catch((response) => alert(response));

    if (!totalPagesCount) {
      return;
    }

    // themoviedb API has changed its max page count query and rate limits
    for (let i = 1; totalPagesCount > 500 ? i <= 500 : i <= totalPagesCount; i++) {
      if (i < 500 && i % 50 === 0) {
        await new Promise((resolve) => setTimeout(resolve, 1100));
      }

      axios
        .get(
          `https://api.themoviedb.org/3/discover/movie?api_key=a1b84ce27d6ea9262430dc19dfd4646c&language=en-US&region=US&sort_by=popularity.desc&include_adult=false&include_video=false&page=${i}&year=${this.yearInput}&with_release_type=3&with_original_language=en`
        )
        .then((response) => {
          this.filmresults.push(response.data.results);
          if (this.filmresults.length === totalPagesCount || this.filmresults.length === 500) {
            this.$emit("update-gotFilmResults", true);
          }
        })
        .catch((error) => {
          alert(error);
        });
    }

    axios
      .get(
        `https://api.themoviedb.org/3/discover/movie?api_key=a1b84ce27d6ea9262430dc19dfd4646c&language=en-US&region=US&sort_by=vote_average.desc&include_adult=false&include_video=false&page=1&primary_release_year=${this.yearInput}&with_release_type=3&vote_count.gte=2000&with_original_language=en`
      )
      .then((response) => {
        this.top10results = response.data.results;
        if (this.top10results.length > 0) {
          this.gottop10results = true;
        }
      })
      .catch((error) => {
        alert(error);
      });
  },
};
</script>

<style></style>
