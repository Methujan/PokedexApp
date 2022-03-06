<template>
  <v-container
    class="pokemonList"
    v-for="pokemon in pokemons"
    :key="pokemon.name"
  >
    <v-row>
      <v-col>
        <img :src="pokemon.sprites.front_default" alt="pokemon.name" />
      </v-col>
      <v-col class="pokemonName mr-3">
        {{ pokemon.name }}
      </v-col>
      <v-col
        class="pokemonTypes"
        v-for="(type, index) in pokemon.types"
        :key="index"
      >
        {{ type.type.name }}
      </v-col>
      <v-col
        class="pokemonStats"
        v-for="(stat, index) in pokemon.stats"
        :key="index"
      >
        {{ stat.base_stat }}
        {{ stat.stat.name }}
      </v-col>
    </v-row>
  </v-container>
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
              console.log([type]);
              type.type.name =
                type.type.name.charAt(0).toUpperCase() +
                type.type.name.slice(1);
              console.log(type);
              // this.capitalizeFirstLetter(pokemonData, [types][type][type]);
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
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  background-color: khaki;
  border-radius: 10px;
}

.pokemonList {
  display: flex;
  align-items: center;
}
.pokemonList > * {
  /* flex: 1;
  flex-basis: 25%; */
}

.pokemonName {
  padding-right: 5vw;
}
.pokemonStats {
  /* padding-left: 10vw; */
  /* display: flex;
  justify-content: space-between; */
}
</style>
