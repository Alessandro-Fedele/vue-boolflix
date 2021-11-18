<template>
  <div class="col">
    <div class="card">
      <img :src="posterUrl" :alt="'poster: ' + title" />
      <div class="card-overlay">
        <p>
          <strong>Titolo: </strong>
          <span>{{ title }}</span>
        </p>
        <p>
          <strong>Titolo originale: </strong>
          <span> {{ originalTitle }}</span>
        </p>
        <p>
          <strong>Lingua originale: </strong>
          <img
            :src="getFlagPath(originalLanguage)"
            :alt="`logo: ` + originalLanguage"
          />
        </p>
        <p>
          <strong>Voto: </strong>
          <RankStar :rank="starsNumber" class="d-inline-block"></RankStar>
        </p>
        <p>
          <strong>Overview </strong> <br />
          <span> {{ overview ? overview : "Overview non disponibile" }}</span>
        </p>
      </div>
    </div>
  </div>
</template>
<script>
import RankStar from "./RankStar.vue";
export default {
  name: "Card",
  components: { RankStar },
  props: {
    title: String,
    originalTitle: String,
    originalLanguage: String,
    rank: Number,
    posterPath: String,
    overview: String,
  },
  data() {
    return {
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
        hu: "hu.png",
        zh: "zh.png",
      },
      posterBasicUrl: "https://image.tmdb.org/t/p/",
      posterSize: "w342",
    };
  },
  methods: {
    getFlagPath(langToSearch) {
      if (!this.flagsXlang[langToSearch]) {
        return require("@/assets/Flags/undefined.png");
      }
      return require("@/assets/Flags/" + this.flagsXlang[langToSearch]);
    },
  },
  computed: {
    posterUrl() {
      if (!this.posterPath) {
        return require("@/assets/missing-img.jpg");
      }
      return this.posterBasicUrl + this.posterSize + this.posterPath;
    },
    starsNumber() {
      return Math.round(this.rank / 2);
    },
  },
};
</script>