/* eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /*
eslint-disable no-unused-vars */ /* eslint-disable no-unused-vars */ /*
eslint-disable no-unused-components */ /* eslint-disable no-unused-components */
/* eslint-disable no-unused-components */ /* eslint-disable no-unused-components
*/

<template>
  <div id="api-fetcher-wrapper">
    <Calendar
      v-if="gotfilmresults"
      v-bind:filmdata="filmresults"
      v-bind:yearInput="yearInput"
    />
    <DataVisualizer v-if="gotfilmresults" v-bind:filmdata="filmresults" />
    <PopularMovies
      v-if="gottop10results && gotfilmresults"
      v-bind:toptendata="top10results"
    />
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
  props: ["yearInput"],
  components: {
    Calendar,
    DataVisualizer,
    PopularMovies,
  },
  data() {
    return {
      gotfilmresults: false,
      gottop10results: false,
      filmresults: [],
      top10results: {},
    };
  },
  mounted() {
    console.log(this.yearInput);
    axios
      .get(
        `https://api.themoviedb.org/3/discover/movie?api_key=a1b84ce27d6ea9262430dc19dfd4646c&language=en-US&region=US&sort_by=popularity.desc&include_adult=false&include_video=false&page=52&year=${this.yearInput}&with_release_type=3&with_original_language=en`
      )
      .then((response) => {
        for (let i = 1; i <= response.data.total_pages; i++) {
          axios
            .get(
              `https://api.themoviedb.org/3/discover/movie?api_key=a1b84ce27d6ea9262430dc19dfd4646c&language=en-US&region=US&sort_by=popularity.desc&include_adult=false&include_video=false&page=${i}&year=${this.yearInput}&with_release_type=3&with_original_language=en`
            )
            .then((response) => {
              this.filmresults.push(response.data.results);
              if (this.filmresults.length === response.data.total_pages) {
                console.log(this.filmresults);
                this.gotfilmresults = true;
              }
            });
        }
      });
    axios
      .get(
        `https://api.themoviedb.org/3/discover/movie?api_key=a1b84ce27d6ea9262430dc19dfd4646c&language=en-US&region=US&sort_by=vote_average.desc&include_adult=false&include_video=false&page=1&primary_release_year=${this.yearInput}&with_release_type=3&vote_count.gte=5000&with_original_language=en`
      )
      .then((response) => {
        this.top10results = response.data.results;
        this.gottop10results = true;
      });
  },
};
</script>

<style></style>
