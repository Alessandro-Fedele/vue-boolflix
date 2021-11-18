<template>
  <div>
    <input v-model="searchInput" type="text" @keydown.enter="startSearch" />
    <button @click="startSearch">Cerca</button>
  </div>
</template>
<script>
export default {
  name: "SearchBar",
  data() {
    return {
      searchInput: "",
    };
  },
  methods: {
    startSearch() {
      this.$emit("search", this.searchInput);
    },
  },
};
</script>