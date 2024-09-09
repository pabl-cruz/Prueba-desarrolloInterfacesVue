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
      showPokemon: false,
      shake: false
    }
  },
  emits: ['addDiscoveredPokemon', 'add-discoveredPokemon'],
  methods: {
    sendInputData() {
      if (this.pokemonInput.toLowerCase() === this.pokemon.name) {
        this.showPokemon = true
        this.shake = false
        this.$emit('add-discoveredPokemon', {
          pokemonInput: this.pokemonInput
        })
      } else {
        this.showPokemon = false
        this.shake = false
        this.$nextTick(() => {
          this.$refs.shakeElement.offsetHeight
          this.shake = true
        })
      }
    }
  }
}
</script>

<template>
  <figure ref="shakeElement">
    <img
      :src="pokemon.details.sprites.front_default"
      :alt="pokemon.name"
      :class="{
        hidden: !showPokemon,
        show: showPokemon,
        shake: shake
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

.shake {
  animation-name: shake;
  animation-duration: 1s;
  animation-fill-mode: both;
}

@keyframes shake {
  0%,
  100% {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
  10%,
  30%,
  50%,
  70%,
  90% {
    -webkit-transform: translate3d(-10px, 0, 0);
    transform: translate3d(-10px, 0, 0);
  }
  20%,
  40%,
  60%,
  80% {
    -webkit-transform: translate3d(10px, 0, 0);
    transform: translate3d(10px, 0, 0);
  }
}
</style>
