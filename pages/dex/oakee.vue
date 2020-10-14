<template>
  <div>
    <H2>My Pokedex Content</H2>
    <v-toolbar>
      <v-text-field v-model="search" label="Search" />
    </v-toolbar>
    <v-layout wrap>
      <v-flex lg2 md3 sm6 xs12 v-for="(pk, idx) in this.filterDex" :key="idx">
        <v-card outlined>
          <v-img
            :src="pk.sprites.animated"
            style="padding: 20px"
            width="150px"
            height="100px"
          />
          <v-title>{{ pk.name }}</v-title>
        </v-card>
      </v-flex>
    </v-layout>
  </div>
</template>
<script>
const URL =
  "https://raw.githubusercontent.com/joseluisq/pokemons/master/pokemons.json";

export default {
  layout: "dexlayout",
  data: () => ({
    pokedex: [],
    search: "",
    filterDex: [],
  }),

  created() {
    console.log("--- created ---");
    this.initialize();
  },

  watch: {
    search(val) {
      this.filterDex = this.pokedex.filter((pk) => {
        return pk.name.indexOf(val) != -1;
      });
    },
  },
  methods: {
    async initialize() {
      try {
        const res = await this.$axios.get(URL);
        console.log("--- init ---");
        console.log(res.data);
        this.pokedex = res.data.results;
        this.filterDex = this.pokedex;
      } catch (err) {
        console.log(err);
      }
    },
    addFav(pk) {
      console.log("--addfav--" + JSON.stringify(pk));
    },
  },
};
</script>