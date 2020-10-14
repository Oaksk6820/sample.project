<template>
  <v-container>
    <v-toolbar flat>
      <v-spacer></v-spacer>
      <v-text-field
        v-model="Search"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
      <v-spacer></v-spacer>
    </v-toolbar>
    <v-layout wrap>
      <v-flex
        pa-1
        lg2
        md3
        sm6
        xs12
        v-for="(pk, idx) in this.filterDex"
        :key="idx"
      >
        <v-fade-transition mode="out-in">
          <v-row>
            <v-col cols="10">
              <v-card>
                <v-img
                  :src="pk.sprites.large"
                  style
                  max-height="100"
                  max-width="120"
                  contain
                  class="grey darken-4"
                ></v-img>
                <v-card-title>{{ pk.name }}</v-card-title>
                <v-card-subtitle>{{ pk.type }}</v-card-subtitle>
                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-icon @click="addFav(pk)">FAV</v-icon>
                </v-card-actions>
              </v-card>
            </v-col>
          </v-row>
        </v-fade-transition>
      </v-flex>
    </v-layout>
  </v-container>
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