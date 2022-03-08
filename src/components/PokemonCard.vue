<template>
  <div class="detail">
    <v-card class="detailView" v-if="show">
      {{ pokemon[0].name }}
      <button @click="closeDetails">Close / Fechar</button>
    </v-card>
  </div>
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
      this.$emit("closeDetails");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.detail {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  position: fixed;
  top: 0;
  left: 0;
  padding: 90px 10px 10px;
  width: calc(100% - 20px);
  height: calc(100vh - 20px);
  width: 100%;
  height: 100vh;
  background: rgba(10, 7, 0, 0.562);
}
.detailView {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 90%;
  padding: 50px 0 0;
  position: relative;

  max-width: 510px;

  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
</style>
