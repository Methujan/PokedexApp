<template>
  <div class="pokemonList">
    <template> </template>
  </div>
</template>

<script>
export default {
  props: ["dataURL"],
  data: () => {
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
    mounted() {
      this.getPokemonData();
    },
    created() {
      this.currentURL = this.dataURL;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
