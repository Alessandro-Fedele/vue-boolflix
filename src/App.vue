<template>
  <div id="app">
    <input v-model="searchInput" type="text" />
    <button @click="search">Cerca</button>
    <h2>Films</h2>
    <ul>
      <li v-for="movie in movies" :key="movie.id">
        <strong>Titolo:</strong> {{ movie.title }} <br />
        <strong>Titolo originale:</strong> {{ movie.original_title }} <br />
        <strong>Lingua:</strong>
        <img
          :src="
            require(`@/assets/Flags/${flagsXlang[movie.original_language]}`)
          "
          alt="img"
        />
        {{ movie.original_language }} <br />
        <strong>Voto:</strong> {{ movie.vote_average }} <br />
      </li>
    </ul>
    <hr />
    <h2>Serie TV</h2>
    <ul>
      <li v-for="serie in series" :key="serie.id">
        <strong>Titolo:</strong> {{ serie.name }} <br />
        <strong>Titolo originale:</strong> {{ serie.original_name }} <br />
        <strong>Lingua:</strong>
        <!-- <img
          :src="require(`@/assets/` + flagsXlang[serie.original_language])"
          alt="img"
        /> -->
        {{ serie.original_language }} <br />
        <strong>Voto:</strong> {{ serie.vote_average }} <br />
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  components: {},
  data() {
    return {
      apiUrl: "https://api.themoviedb.org/3",
      apiKey: "41150d102d7f7cd4fe50876e84547deb",
      movies: [],
      series: [],
      searchInput: "",
      flagsXlang: {
        en: "en.png",
        it: "it.png",
        es: "es.png",
        pt: "pt.png",
        de: "de.png",
        ja: "ja.png",
        fr: "fr.png",
        ru: "ru.png",
        tr: "tr.png",
        hi: "hi.png",
      },
    };
  },
  methods: {
    searchQuery(url, query, dataKey) {
      axios
        .get(this.apiUrl + url, {
          params: {
            api_key: this.apiKey,
            query: query,
            language: "it",
          },
        })
        .then((resp) => {
          this[dataKey] = resp.data.results;
        });
    },
    search() {
      this.searchQuery("/search/movie", this.searchInput, "movies");
      this.searchQuery("/search/tv", this.searchInput, "series");
    },
  },
  mounted() {
    // Ricerca tra i film
    // this.searchQuery("/search/movie", "ciao", "movies");
    // Ricerca tra serie tv
    // this.searchQuery("/search/tv", "ciao", "series");
    // --------------------------------------------------
    // axios
    //   .get(this.apiUrl + "/search/movie", {
    //     params: {
    //       api_key: this.apiKey,
    //       query: "casa",
    //     },
    //   })
    //   .then((resp) => {
    //     this.movies = resp.data.results;
    //   });
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  li {
    border: 1px solid black;
    margin-bottom: 10px;
    padding: 10px;
    img {
      width: 35px;
    }
  }
}
</style>
