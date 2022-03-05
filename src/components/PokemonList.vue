<template>
  <div class="pokemonList" v-for="pokemon in pokemons" :key="pokemon.name">
    <img :src="pokemon.sprites.front_default" alt="pokemon.name" />
    <div class="pokemonName">
      {{ pokemon.name }}
    </div>
    <div class="types" v-for="(type, index) in pokemon.types" :key="index">
      {{ type.type.name }}
    </div>
    <div class="stats" v-for="(stat, index) in pokemon.stats" :key="index">
      {{ stat.base_stat }}
      {{ stat.stat.name }}
    </div>
  </div>
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

.pokemonName {
  padding-right: 7vw;
}
</style>
