<template>
  <div class="pokemonList" v-for="pokemon in pokemons" :key="pokemon.url">
    <img :src="pokemon.sprites.front_default" alt="pokemon.name" />
    {{ pokemon.name }}
    <div class="types" v-for="(type, index) in pokemon.types" :key="index">
      {{ type.type.name }}
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
          this.pokemons.push(pokemonData);
        });
      console.log(this.pokemons);
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
}
.pokemonList {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
