<template>
  <div>
    <span v-for="n in rank" :key="n + `fill`"
      ><i class="fa fa-star" aria-hidden="true"></i
    ></span>
    <span v-for="n in emptyStars" :key="n + `empty`"
      ><i class="fa fa-star-o" aria-hidden="true"></i
    ></span>
  </div>
</template>

<script>
export default {
  name: "RankStar",
  props: {
    rank: Number,
  },
  data() {
    return { maxRank: 5 };
  },
  computed: {
    emptyStars() {
      return this.maxRank - this.rank;
    },
  },
};
</script>

<style>
</style>