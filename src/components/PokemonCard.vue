<template>
  <v-card v-if="show">
    {{ pokemon[0].name }}
    <button @click="closeDetails">Close / Fechar</button>
  </v-card>
  <!-- <v-card v-for="pokemon in pokemons" :key="pokemon.name">
    <v-row>
      <v-col></v-col>
    </v-row>
    <v-row class="pokemonList">
      <v-col>
        <img :src="pokemon.sprites.front_default" alt="pokemon.name" />
      </v-col>
      <v-col class="pokemonName">
        {{ pokemon.name }}
      </v-col>
      <div v-if="pokemon.types.length > 1">
        <v-col
          class="pokemonTypes"
          v-for="(type, index) in pokemon.types"
          :key="index"
        >
          <p>
            {{ type.type.name }}
          </p>
        </v-col>
      </div>
      <div v-if="pokemon.types.length == 1">
        <v-col> {{ pokemon.types[0].type.name }}</v-col>
      </div>

      <v-col
        class="pokemonStats"
        v-for="(stat, index) in pokemon.stats"
        :key="index"
      >
        {{ stat.base_stat }}
        {{ stat.stat.name }}
      </v-col>
    </v-row>
  </v-card> -->
</template>

<script>
export default {
  name: "PokemonCard",
  props: ["pokemon"],
  data() {
    return {
      pokemons: [],
      show: true,
    };
  },
  methods: {
    capitalizeFirstLetter(data, key) {
      data[key] = data[key].charAt(0).toUpperCase() + data[key].slice(1);
      return data[key];
    },
    closeDetails() {
      console.log("CLOSEE");
      this.$emit("closeDetails");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
