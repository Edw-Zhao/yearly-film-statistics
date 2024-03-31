<template>
  <div class="component-wrapper">
    <h1 class="header">Notable Movies</h1>
    <p class="note">
      All films presented below are the most popular movies for this year, with the criteria of >2000 votes and are sorted by their rating
      average:
    </p>
    <div class="top-ten-wrapper" v-if="gotimages">
      <template v-for="n in toptendata.length">
        <div class="top-ten-stats" v-bind:key="n">
          <img :src="imgsrc[n - 1]" />
          <div class="details">
            <p><strong style="color: #c40a2f"> Title: </strong>{{ toptendata[n - 1].title }}.</p>
            <p><strong style="color: #c40a2f">Description: </strong>{{ toptendata[n - 1].overview }}</p>
            <p>
              <strong style="color: #c40a2f">Genre(s): </strong
              ><span v-for="i in toptendata[n - 1].genre_ids.length" v-bind:key="'genre' + i">
                {{
                  genreArray[n - 1].length === 1
                    ? genreArray[n - 1][i - 1] + "."
                    : i === genreArray[n - 1].length
                    ? "and " + genreArray[n - 1][i - 1] + "."
                    : genreArray[n - 1].length - i === 1
                    ? genreArray[n - 1][i - 1]
                    : genreArray[n - 1][i - 1] + ","
                }}
              </span>
            </p>
            <p><strong style="color: #c40a2f">Rating Average: </strong>{{ toptendata[n - 1].vote_average }}/10.</p>
            <p><strong style="color: #c40a2f"> Rating Count: </strong>{{ toptendata[n - 1].vote_count }}.</p>
            <p><strong style="color: #c40a2f">Release Date: </strong>{{ toptendata[n - 1].release_date }}.</p>
          </div>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  props: ["toptendata"],
  data() {
    return {
      imgsrc: [""],
      gotimages: false,
      genreArray: [[], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], [], []],
    };
  },
  mounted() {
    for (let i = 0; i < this.toptendata.length; i++) {
      this.toptendata[i].genre_ids.forEach((id) => {
        if (id === 28) {
          this.genreArray[i].push("Action");
        }
        if (id === 12) {
          this.genreArray[i].push("Adventure");
        }
        if (id === 16) {
          this.genreArray[i].push("Animation");
        }
        if (id === 35) {
          this.genreArray[i].push("Comedy");
        }
        if (id === 80) {
          this.genreArray[i].push("Crime");
        }
        if (id === 99) {
          this.genreArray[i].push("Documentary");
        }
        if (id === 18) {
          this.genreArray[i].push("Drama");
        }
        if (id === 10751) {
          this.genreArray[i].push("Family");
        }
        if (id === 14) {
          this.genreArray[i].push("Fantasy");
        }
        if (id === 36) {
          this.genreArray[i].push("History");
        }
        if (id === 27) {
          this.genreArray[i].push("Horror");
        }
        if (id === 10402) {
          this.genreArray[i].push("Music");
        }
        if (id === 9648) {
          this.genreArray[i].push("Mystery");
        }
        if (id === 10749) {
          this.genreArray[i].push("Romance");
        }
        if (id === 878) {
          this.genreArray[i].push("Science Fiction");
        }
        if (id === 10770) {
          this.genreArray[i].push("TV Movie");
        }
        if (id === 53) {
          this.genreArray[i].push("Thriller");
        }
        if (id === 10752) {
          this.genreArray[i].push("War");
        }
        if (id === 37) {
          this.genreArray[i].push("Western");
        }
      });
    }

    for (let i = 0; i < this.toptendata.length; i++) {
      this.imgsrc[i] = "https://image.tmdb.org/t/p/w500" + this.toptendata[i].poster_path;
    }
    this.gotimages = true;
  },
};
</script>

<style scoped>
.component-wrapper {
  background-image: linear-gradient(rgb(36, 36, 36), rgb(0, 0, 0));
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding-bottom: 80px;
}
p {
  margin-top: 5px;
}
img {
  width: 100%;
  border: solid 2px yellow;
  box-shadow: 0 0 15px #e5ed9e;
  margin-bottom: 5px;
}
.top-ten-wrapper {
  display: grid;
  width: 100%;
  grid-template-columns: 20% 20% 20% 20% 20%;
  padding-top: 40px;
}
.top-ten-stats {
  padding: 10px;
  display: flex;
  flex-direction: column;
  color: white;
  font-size: 14px;
}

@media only screen and (max-width: 600px) {
  .top-ten-wrapper {
    grid-template-columns: 50% 50%;
  }
}

@media only screen and (max-width: 1200px) and (min-width: 600px) {
  .top-ten-wrapper {
    grid-template-columns: 25% 25% 25% 25%;
  }
}
</style>
