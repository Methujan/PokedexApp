<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/pngwing.com.png" />
    <SearchPokemon msg="Welcome to Your Vue.js App" />
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
