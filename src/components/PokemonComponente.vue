<template>
    <div class="pokemon-item">
      <img :src="imagenUrl" alt="Pokemon" :style="{ filter: descubierto ? 'none' : filtro }" />
      <div v-if="!descubierto">
        <input type="text" v-model="nombreIngresado" />
        <button @click="verificarNombre">Descubrir</button>
      </div>
      <p v-else>{{ pokemon.name }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: "PokemonComponente",
    props: {
      pokemon: Object,
    },
    data() {
      return {
        nombreIngresado: "",
        filtro: "blur(5px) grayscale(100%)",
        descubierto: false, // Estado local para manejar si el Pokémon está descubierto
      };
    },
    computed: {
      imagenUrl() {
        return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${this.getPokemonId()}.png`;
      },
    },
    methods: {
      verificarNombre() {
        if (this.nombreIngresado.toLowerCase() === this.pokemon.name.toLowerCase()) {
          this.descubierto = true;
          this.$emit("descubierto");
        } else {
          alert("Incorrecto. Inténtalo de nuevo.");
        }
      },
      getPokemonId() {
        return this.pokemon.url.split("/")[6];
      },
    },
  };
  </script>
  
  <style>
  /* Estilos para PokemonComponente.vue */
  .pokemon-item {
    text-align: center;
  }
  
  img {
    width: 150px;
    height: 150px;
    margin-bottom: 10px;
  }
  
  input {
    margin-bottom: 10px;
  }
  
  button {
    background-color: #4caf50;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #45a049;
  }
  </style>
  