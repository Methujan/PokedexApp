<template>
  <div class="search">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="term" @click="getPokemon" />
    <div>
      <img :src="result.imgs" :alt="result.name" />
      {{ result.name }}
      <template v-for="ability in result.abilities">
        {{ ability }}
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
      term: "",
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
    getPokemon() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.term}`)
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          console.log(data.name);
          this.result.name = data.name;
          this.result.imgs = data.sprites.front_shiny;
          this.result.height = data.height;
          this.result.weight = data.weight;
          data.abilities.forEach((ability) => {
            this.result.abilities.push(ability.name);
            console.log("ability", ability.ability.name);
            console.log("abilityreslt", this.results.abilities);
          });
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
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
</style>
