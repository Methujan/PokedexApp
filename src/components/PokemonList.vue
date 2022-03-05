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
      console.log(url);
      fetch(url)
        .then((res) => res.json())
        .then((pokemonData) => {
          if (pokemonData.name) {
            // newPokemonData = this.capitalizeFirstLetter(pokemonData);
            pokemonData.name =
              pokemonData.name.charAt(0).toUpperCase() +
              pokemonData.name.slice(1);
            console.log(
              pokemonData.name.charAt(0).toUpperCase() +
                pokemonData.name.slice(1)
            );
            // console.log("newPokeo", newPokemonData);
            console.log("pokemon", pokemonData.name);
          }
          this.pokemons.push(pokemonData);
          console.log(pokemonData);
        });
    },
    capitalizeFirstLetter(obj) {
      // console.log(obj.name.charAt(0).toUpperCase() + obj.name.slice(1));
      const newObj = obj;
      newObj.name.charAt(0).toUpperCase() + newObj.name.slice(1);
      return newObj;
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
