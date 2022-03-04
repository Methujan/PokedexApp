<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/pngwing.com.png" />
    <SearchPokemon msg="Enter a Pokemon" />
    <PokemonList :dataURL="dataURL" />
  </div>
</template>

<script>
// @ is an alias to /src
import SearchPokemon from "@/components/SearchPokemon.vue";
import PokemonList from "@/components/PokemonList.vue";

export default {
  name: "HomeView",
  components: {
    SearchPokemon,
    PokemonList,
  },
  data() {
    return {
      dataURL: "https://pokeapi.co/api/v2/pokemon/",
    };
  },
  methods: {
    setURL(url) {
      this.pokemonURL = url;
    },
    closeDetail() {
      this.pokemonURL = "";
    },
  },
};
</script>
