<template>
  <v-card v-for="pokemon in pokemons" :key="pokemon.name">
    <v-row>
      <v-col></v-col>
    </v-row>
    <v-row class="pokemonList">
      <v-col>
        <img :src="pokemon.sprites.front_default" alt="pokemon.name" />
      </v-col>
      <v-col class="pokemonName">
        {{ pokemon.name }}
      </v-col>
      <div v-if="pokemon.types.length > 1">
        <v-col
          class="pokemonTypes"
          v-for="(type, index) in pokemon.types"
          :key="index"
        >
          <p>
            {{ type.type.name }}
          </p>
        </v-col>
      </div>
      <div v-if="pokemon.types.length == 1">
        <v-col> {{ pokemon.types[0].type.name }}</v-col>
      </div>

      <v-col
        class="pokemonStats"
        v-for="(stat, index) in pokemon.stats"
        :key="index"
      >
        {{ stat.base_stat }}
        {{ stat.stat.name }}
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
export default {
  name: "PokemonList",
  props: ["dataURL"],
  data() {
    return {
      pokemons: [],
      nextURL: "",
      currentURL: "",
    };
  },
  methods: {
    getAllPokemonData() {
      fetch(this.currentURL)
        .then((res) => res.json())
        .then((data) => {
          data.results.forEach((pokemon) => {
            this.getEachPokemonData(pokemon);
          });
        });
    },
    getEachPokemonData(pokemon) {
      let url = pokemon.url;
      fetch(url)
        .then((res) => res.json())
        .then((pokemonData) => {
          if (pokemonData.name) {
            this.capitalizeFirstLetter(pokemonData, "name");
          }
          if (pokemonData.types) {
            pokemonData.types.forEach((type) => {
              type.type.name =
                type.type.name.charAt(0).toUpperCase() +
                type.type.name.slice(1);
              // this.capitalizeFirstLetter(pokemonData, [types][type][type]);
            });
          }
          if (pokemonData.stats.base_stat) {
            console.log(pokemonData.stats.base_stat);
            pokemonData.stats.forEach((stat) => {
              stat.base_stat =
                stat.base_stat.charAt(0).toUpperCase() +
                stat.base_stat.slice(1);
            });
          }
          this.pokemons.push(pokemonData);
        });
    },
    capitalizeFirstLetter(data, key) {
      data[key] = data[key].charAt(0).toUpperCase() + data[key].slice(1);
      return data[key];
    },
  },
  mounted() {
    this.getAllPokemonData();
  },
  created() {
    this.currentURL = this.dataURL;
    console.log(this.pokemons);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  background-color: khaki;
}

.pokemonList {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}

.pokemonName {
  /* padding: auto; */
}
.pokemonStats {
  /* padding: auto; */
}
</style>
