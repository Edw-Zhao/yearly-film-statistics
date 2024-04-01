<template>
  <div class="main">
    <div
      class="year-input-wrapper"
      v-bind:style="[
        gotFilmResults
          ? {
              'padding-top': '40px',
              'padding-bottom': '40px',
            }
          : null,
      ]"
    >
      <div class="screen">
        <input
          class="year-input"
          type="number"
          min="1900"
          max="2020"
          v-model="readYearInput"
          placeholder="Enter Year"
          @keyup.enter="
            if (readYearInput >= 1900 && readYearInput <= new Date().getFullYear()) {
              yearInput = readYearInput;
              gotFilmResults = false;
              wrongInput = false;
            } else {
              wrongInput = true;
            }
          "
        />
        <div v-if="wrongInput" class="alert">Enter a valid year: (1900 - {{ new Date().getFullYear() }})</div>
        <div v-else class="empty-space"></div>
        <button
          class="submit-year"
          v-on:click="
            if (readYearInput >= 1900 && readYearInput <= new Date().getFullYear()) {
              yearInput = readYearInput;
              gotFilmResults = false;
              wrongInput = false;
            } else {
              wrongInput = true;
            }
          "
        >
          Display Data
        </button>
      </div>
      <div class="seats-wrapper">
        <div class="cinema-seats left">
          <div class="cinema-row row-1">
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
          </div>
          <div class="cinema-row row-2">
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
          </div>
          <div class="cinema-row row-3">
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
          </div>
          <div class="cinema-row row-4">
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
          </div>
          <div class="cinema-row row-5">
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
          </div>
        </div>
        <div class="cinema-seats left mirror">
          <div class="cinema-row row-1">
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
          </div>

          <div class="cinema-row row-2">
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
          </div>

          <div class="cinema-row row-3">
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
          </div>

          <div class="cinema-row row-4">
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
          </div>

          <div class="cinema-row row-5">
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
            <div class="seat"></div>
          </div>
        </div>
      </div>
    </div>
    <ApiFetcher
      v-bind:yearInput="yearInput"
      v-bind:gotFilmResults="gotFilmResults"
      v-if="yearInput"
      @update-gotFilmResults="handleUpdateGotFilmResults"
    />
    <div
      class="info"
      v-bind:style="[
        gotFilmResults
          ? {
              'background-image': 'none',
              'background-color': 'rgb(0, 0, 0)',
              color: 'white',
            }
          : null,
      ]"
    >
      <p v-if="yearInput && !gotFilmResults" class="description loading">
        <span class="loader"></span>
        Loading... This will take approximately 10 seconds.
      </p>
      <p class="description">
        This is a simple API project that displays statistics of theatrical film releases for the desired input year for the first 10000
        movies sorted by descending popularity due to the API service limits. The data presented are borrowed from
        <a href="https://developers.themoviedb.org/" target="_blank" rel="noopener noreferrer">The Movie Database.</a>
      </p>
      <p class="description">
        This was a learning experience for me to simultaneously learn JSON data handling with Vue.js as a new framework to reach my
        aspirations of a career in front-end development.
      </p>
      <div class="contact-details">
        <a href="https://github.com/Edw-Zhao" target="_blank" rel="noopener noreferrer">
          <font-awesome-icon :icon="['fab', 'github-square']" class="icon" />
        </a>
        <a href="https://www.linkedin.com/in/edward-lu-zhao/" target="_blank" rel="noopener noreferrer">
          <font-awesome-icon :icon="['fab', 'linkedin']" class="icon" />
        </a>

        <font-awesome-icon icon="envelope-square" class="icon" v-on:click="showEmail = true" />
      </div>
      <p class="email" v-if="showEmail">Edward.Zhao@Dal.ca</p>
    </div>
  </div>
</template>

<script>
import ApiFetcher from "./ApiFetcher.vue";
export default {
  name: "App",
  components: {
    ApiFetcher,
  },
  data() {
    return {
      readYearInput: "",
      yearInput: 0,
      wrongInput: false,
      showEmail: false,
      gotFilmResults: false,
    };
  },
  methods: {
    handleUpdateGotFilmResults(gotFilmResults) {
      this.gotFilmResults = gotFilmResults;
    },
  },
};
</script>

<style>
* {
  margin: 0;
}

html,
body {
  height: 100%;
}

.header {
  color: rgb(61, 47, 255);
  font-size: 24px;
  margin-bottom: 30px;
  border-bottom: 2px solid rgb(119, 0, 0);
  width: 80%;
  box-shadow: rgb(252, 255, 213) 0px 3px 2px -2px;
}

.main {
  display: flex;
  flex-direction: column;
  padding-top: 20px;
  height: 100%;
  width: 100%;
}

.year-input-wrapper {
  height: 250px;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  display: flex;
  padding-top: 150px;
  background-image: linear-gradient(white, rgb(236, 236, 236));
}

.screen {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 150px;
  width: 275px;
  box-shadow: 0 0 30px #000000;
  background-color: rgb(34, 34, 34);
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type="number"] {
  -moz-appearance: textfield;
  padding: 0px;
}

.year-input {
  height: 50px;
  width: 150px;
  text-align: center;
  font-size: 30px;
  border: solid 2px yellow;
  box-shadow: 0 0 20px red;
  outline: none;
  color: #000000;
  background-color: rgb(255, 255, 255);
  display: flex;
}

.alert {
  color: white;
  padding: 0;
  margin: 0;
  height: 20px;
  padding-top: 5px;
}

.empty-space {
  height: 25px;
}

.submit-year {
  height: 25px;
  width: 110px;
  font-size: 16px;
  background-color: #c40a2f;
  color: white;
  border: solid 1px yellow;
}

.submit-year:hover {
  background-color: black;
}

.submit-year:focus {
  outline: none;
  border: solid 1px black;
}

.seats-wrapper {
  display: flex;
  justify-content: center;
  padding-top: 50px;
}

.note {
  text-align: center;
  margin-top: 40px;
  font-size: 16px;
  color: #c40a2f;
  font-style: italic;
  font-weight: bold;
}

.info {
  text-align: center;
  width: 100%;
  font-size: 20px;
  padding-top: 20px;
  background-image: linear-gradient(rgb(236, 236, 236), rgb(0, 0, 0));
  color: black;
  vertical-align: center;
  display: flex;
  align-items: center;
  flex-direction: column;
  flex-grow: 1;
  padding-bottom: 50px;
}

.description {
  margin-top: 20px;
  text-align: start;
  width: 80%;
  max-width: 1000px;

  &.loading {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 16px;
    margin-bottom: 10px;
  }

  .loader {
    width: 48px;
    height: 48px;
    border: 5px solid #fff;
    border-bottom-color: #c40a2f;
    border-radius: 50%;
    display: inline-block;
    box-sizing: border-box;
    animation: rotation 1s linear infinite;
  }
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes transition {
  0% {
    background-image: linear-gradient(rgb(236, 236, 236), rgb(0, 0, 0));
    color: black;
  }
  100% {
    background-image: linear-gradient(rgb(0, 0, 0), rgb(0, 0, 0));
    color: white;
  }
}

.icon {
  padding: 0;
  margin: 20px;
  font-size: 40px;
  color: #c40a2f;
}

.icon:hover {
  color: yellow;
}

.cinema-seats {
  display: flex;
  justify-content: center;
}

.mirror {
  transform: scaleX(-1);
  margin-left: 30px;
}
.cinema-seats .seat:hover:before {
  content: "";
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  border-radius: 7px;
}
.cinema-seats .seat.active:before {
  content: "";
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.6);
  border-radius: 7px;
}

.left .cinema-row {
  width: 15px;
  transform: skew(-15deg);
  margin: 0 6px;
}
.left .seat {
  width: 20px;
  height: 35px;
  border-radius: 7px;
  background: linear-gradient(to top, #881b1b, #881b1b, #881b1b, #881b1b, #881b1b, #ca474a, #fa6b6e);
  margin-bottom: 10px;
  transform: skew(20deg);
  margin-top: -32px;
  box-shadow: 0 0 40px rgba(0, 0, 0, 0.5);
}
.left .row-2 {
  transform: skew(-13deg);
}
.left .row-2 .seat {
  transform: skew(18deg);
}
.left .row-3 {
  transform: skew(-12deg);
}
.left .row-3 .seat {
  transform: skew(16deg);
}
.left .row-4 {
  transform: skew(-11deg);
}
.left .row-4 .seat {
  transform: skew(15deg);
}
.left .row-5 {
  transform: skew(-10deg);
}
.left .row-5 .seat {
  transform: skew(12deg);
}

.email {
  color: #c40a2f;
}

@media only screen and (max-width: 600px) {
  .year-input-wrapper {
    padding-top: 40px;
    padding-bottom: 40px;
  }
  .alert {
    font-size: 14px;
    height: 20px;
    padding-top: 5px;
  }
  .info {
    text-align: center;
    width: 100%;
    font-size: 16px;
    padding-top: 20px;
    padding-bottom: 70px;
  }
  .header {
    font-size: 22px;
    width: 95%;
  }
}
</style>
