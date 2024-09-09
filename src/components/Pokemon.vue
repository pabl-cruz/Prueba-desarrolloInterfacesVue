<script>
export default {
  name: 'PokemonComponent',
  props: {
    pokemon: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      pokemonInput: ''
    }
  },
  methods: {
    sendInputData() {
      if (this.pokemonInput) {
        console.log(this.pokemonInput)
      }
    }
  }
}
</script>

<template>
  <figure>
    <img :src="pokemon.details.sprites.front_default" :alt="pokemon.name" />
  </figure>
  <h4>{{ pokemon.name }}</h4>
  <input type="text" v-model="pokemonInput" />
  <button @click="sendInputData()">Descubrir</button>
</template>

<style scoped>
div {
  margin: 0 auto;
  display: flex;
  justify-content: center;
}
p,
h4 {
  text-align: center;
}

figure {
  display: flex;
  justify-content: center;
}

img {
  width: 150px;
}

h4 {
  font-weight: bold;
}
</style>
