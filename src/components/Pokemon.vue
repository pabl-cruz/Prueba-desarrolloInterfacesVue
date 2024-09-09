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
      pokemonInput: '',
      showPokemon: false
    }
  },
  methods: {
    sendInputData() {
      if (this.pokemonInput.toLowerCase() === this.pokemon.name) {
        console.log(this.pokemonInput)
        console.log('lo hiciste ;)')
        this.showPokemon = true
      } else {
        console.log('error, intenta de nuevo')
        this.showPokemon = false
      }
    }
  }
}
</script>

<template>
  <figure>
    <img
      :src="pokemon.details.sprites.front_default"
      :alt="pokemon.name"
      :class="{
        hidden: showPokemon === false,
        show: showPokemon === true
      }"
    />
  </figure>
  <h4 v-show="showPokemon">{{ pokemon.name }}</h4>
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

.hidden {
  filter: blur(5px) grayscale(100%);
}
.show {
  animation: unfade;
  animation-duration: 0.61s;
  animation-timing-function: ease;
}

@keyframes unfade {
  from {
    filter: blur(5px) grayscale(100%);
  }
  to {
    filter: blur(none) grayscale(0%);
  }
}
</style>
