<script>
import axios from 'axios'
import HeaderComponent from '@/components/Header.vue'
import PokemonComponent from '@/components/Pokemon.vue'
export default {
  components: {
    HeaderComponent,
    PokemonComponent
  },
  //fetch lista de pokemons al iniciar app
  async mounted() {
    try {
      const url = 'https://pokeapi.co/api/v2/pokemon?limit=20'
      const { data } = await axios.get(url)
      const pokemon = data.results
      const detailedPokeData = pokemon.map(async (obj, index) => {
        const pokemonDetail = await axios.get(obj.url)
        return {
          name: obj.name,
          pokeId: index,
          details: pokemonDetail.data
        }
      })
      const pokeData = await Promise.all(detailedPokeData)
      this.pokeData = pokeData
      console.log(pokeData)
    } catch (error) {
      console.error('Error al hacer fetch de datos:', error)
    }
  },
  data() {
    return {
      pokeData: ''
    }
  }
}
</script>

<template>
  <HeaderComponent />
  <div class="row">
    <div v-for="(pokemon, id) in pokeData" :key="id" class="pokemon">
      <PokemonComponent :pokemon="pokemon" />
    </div>
  </div>
</template>

<style scoped>
.row {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.pokemon {
  margin: 1rem 1.75rem;
}
</style>
