<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/pngwing.com.png" />
    <SearchPokemon msg="Enter a Pokemon" />
  </div>
</template>

<script>
// @ is an alias to /src
import SearchPokemon from "@/components/SearchPokemon.vue";

export default {
  name: "HomeView",
  components: {
    SearchPokemon,
  },
};
</script>
