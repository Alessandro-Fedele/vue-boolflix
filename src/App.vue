<template>
  <div id="app">
    <header>
      <nav>
        <span>BOOLFLIX</span>
        <SearchBar @search="search"></SearchBar>
      </nav>
    </header>
    <div class="container">
      <h2 v-if="movies.length > 0">Films</h2>
      <div class="row row-cols-2 row-cols-md-3">
        <Card
          v-for="movie in movies"
          :key="movie.id"
          :title="movie.title"
          :originalTitle="movie.original_title"
          :originalLanguage="movie.original_language"
          :rank="movie.vote_average"
          :posterPath="movie.poster_path"
          :overview="movie.overview"
        ></Card>
      </div>
      <h2 v-if="series.length > 0">Serie TV</h2>
      <div class="row row-cols-2 row-cols-md-3">
        <Card
          v-for="serie in series"
          :key="serie.id"
          :title="serie.name"
          :originalTitle="serie.original_name"
          :originalLanguage="serie.original_language"
          :rank="serie.vote_average"
          :posterPath="serie.poster_path"
          :overview="serie.overview"
        ></Card>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar.vue";
import Card from "./components/Card.vue";
export default {
  name: "App",
  components: { SearchBar, Card },
  data() {
    return {
      apiUrl: "https://api.themoviedb.org/3",
      apiKey: "41150d102d7f7cd4fe50876e84547deb",
      movies: [],
      series: [],
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
    // la funzione search riceve come argomento i dati mandati dall'emit, cioè l'input
    search(searchInput) {
      this.searchQuery("/search/movie", searchInput, "movies");
      this.searchQuery("/search/tv", searchInput, "series");
    },
  },
};
</script>

<style lang="scss">
@import "@/styles/app";
</style>