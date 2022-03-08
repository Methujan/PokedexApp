<template>
  <PokemonCard
    v-if="showDetail"
    :pokemon="pokemon"
    @closeDetails="closeDetails"
  />
  <div class="search">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="query" />
    <button type="submit" @click="getPokemon">Search</button>
  </div>
</template>

<script>
import PokemonCard from "@/components/PokemonCard.vue";
export default {
  name: "SearchPokemon",
  props: {
    msg: String,
  },
  components: {
    PokemonCard,
  },
  data() {
    return {
      results: { name: "", imgs: "" },
      pokemon: [],
      query: "",
      showDetail: false,
    };
  },
  methods: {
    capitalizeFirstLetter(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },
    getPokemon() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.query}`)
        .then((response) => response.json())
        .then((data) => {
          this.showDetail = true;
          console.log(data);
          this.pokemon = [];
          this.pokemon.push(data);
          console.log(this.pokemon);
          // this.result.name = data.name;
          // this.result.imgs = data.sprites.front_shiny;
          // data.types.forEach((typedata) => {
          //   this.result.types.push(typedata.type.name);
          // });
          // this.result.height = data.height;
          // this.result.weight = data.weight;
          // data.abilities.forEach((ability) => {
          //   this.result.abilities.push(ability.ability.name);
          // });
        });
    },
    closeDetails() {
      this.showDetail = false;
      console.log("yeyeyeye");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.pokemonResults {
  background: khaki;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.pokemonTypes {
  border: 10px;
}
</style>
