<template>
    <div>
      <p>Pokémon descubiertos: {{ contador }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: "ContadorComponente",
    props: {
      contador: Number,
    },
  };
  </script>
  
  <style>
  /* Estilos para ContadorComponente.vue */
  p {
    text-align: center;
  }
  </style>
  