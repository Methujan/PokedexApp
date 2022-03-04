<template>
  <div class="pokemonList" v-for="pokemon in pokemons" :key="pokemon.url">
    {{ pokemon.name }}
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
    getPokemonData() {
      fetch(this.currentURL)
        .then((res) => res.json())
        .then((data) => {
          console.log(data);
          data.results.forEach((pokemon) => {
            console.log(pokemon);
            this.pokemons.push(pokemon);
          });
        });
    },
  },
  mounted() {
    this.getPokemonData();
  },
  created() {
    this.currentURL = this.dataURL;
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
