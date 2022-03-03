<template>
  <div class="search">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="term" />
    <button type="submit" @click="getPokemon">Search</button>
    <div class="pokemonResults">
      <img :src="result.imgs" :alt="result.name" />
      <h3>
        {{ result.name }}
      </h3>
      <template v-for="ability in result.abilities" :key="ability">
        <h5>
          {{ ability }}
        </h5>
      </template>
      <template v-for="type in result.types" :key="type">
        <div class="pokemonTypes">
          <h5>
            {{ type }}
          </h5>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchPokemon",
  props: {
    msg: String,
  },
  data() {
    return {
      term: null,
      result: {
        name: "",
        imgs: [],
        height: null,
        weight: null,
        abilities: [],
        types: [],
      },
    };
  },
  methods: {
    capitalizeFirstLetter(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },
    getPokemon() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.term}`)
        .then((response) => response.json())
        .then((data) => {
          this.result.name = this.capitalizeFirstLetter(data.name);
          this.result.imgs = data.sprites.front_shiny;
          data.types.forEach((typedata) => {
            this.result.types.push(typedata.type.name);
          });
          this.result.height = data.height;
          this.result.weight = data.weight;
          data.abilities.forEach((ability) => {
            this.result.abilities.push(ability.ability.name);
          });
        });
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
