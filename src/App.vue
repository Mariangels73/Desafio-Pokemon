<template>
  <div>
    <div class="header">
      <img src="./assets/logopokemon.png" height="200px" width="600px" alt="">
      <h1>¡Adivina el Pokémon!</h1>
    </div>
    <contador-componente :contador="contador" />
    <div class="pokemon-grid">
      <pokemon-componente
        v-for="(pokemon, index) in pokemones"
        :key="index"
        :pokemon="pokemon"
        @descubierto="incrementarContador"
      />
    </div>
  </div>
</template>

<script>
import ContadorComponente from "./components/ContadorComponente.vue";
import PokemonComponente from "./components/PokemonComponente.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    ContadorComponente,
    PokemonComponente,
  },
  data() {
    return {
      pokemones: [],
      contador: 0,
    };
  },
  mounted() {
    this.fetchPokemones();
  },
  methods: {
    fetchPokemones() {
      axios
        .get("https://pokeapi.co/api/v2/pokemon?limit=20")
        .then((response) => {
          this.pokemones = response.data.results;
        })
        .catch((error) => {
          console.error("Error fetching Pokémon:", error);
        });
    },
    incrementarContador() {
      this.contador++;
    },
  },
};
</script>

<style>
/* Estilos para App.vue */
.header {
  text-align: center;
  margin-bottom: 20px;
}

.header-logo {
  width: 150px;
  margin-bottom: 10px;
}

h1 {
  margin-bottom: 20px;
}

.pokemon-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  padding: 20px;
}
</style>
