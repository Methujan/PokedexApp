<template>
  <div class="search">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="term" />
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
        name: String,
        imgs: [],
        height: Number,
        weight: Number,
        abilities: [],
        types: [],
      },
    };
  },
  methods: {
    getPokemon() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.getTerm}`)
        .then((response) => {
          response.json();
        })
        .then((data) => {
          console.log(data);
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
