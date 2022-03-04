<template>
  <div class="pokemonList">
    <p>yeeeah</p>
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
        });
    },
  },
  mounted() {
    console.log(this.currentURL);
    this.getPokemonData();
  },
  created() {
    console.log(this.currentURL);
    this.currentURL = this.dataURL;
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
