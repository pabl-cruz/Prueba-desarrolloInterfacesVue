<script>
import axios from 'axios'
import HeaderComponent from '@/components/Header.vue'
import PokemonComponent from '@/components/Pokemon.vue'
export default {
  components: {
    HeaderComponent,
    PokemonComponent
  },
  //fetch lista de pokemones al iniciar app
  async mounted() {
    try {
      const url = 'https://pokeapi.co/api/v2/pokemon?limit=20'
      const { data } = await axios.get(url)
      const pokemon = data.results
      //mapear resultado en arreglo que contenga id y datos de pokemon de url a propiedad
      const detailedPokeData = pokemon.map(async (pokemon, index) => {
        const pokemonDetail = await axios.get(pokemon.url)
        return {
          name: pokemon.name,
          pokeId: index,
          details: pokemonDetail.data
        }
      })
      //asignar constante pokeData a mapeo nuevo una vez se cumpla promesa
      const pokeData = await Promise.all(detailedPokeData)
      this.pokeData = pokeData
    } catch (error) {
      console.error('Error al hacer fetch de datos:', error)
    }
  },
  data() {
    //variables de estado, pokeData es arreglo con datos de los 20 pokemones, pokemons es arreglo de pokemones descubiertos
    return {
      pokeData: '',
      pokemons: []
    }
  },
  methods: {
    //agregar pokemon descubierto a arreglo pokemons una vez esuchado emit de componente hijo
    addDiscoveredPokemon(pkmn) {
      this.pokemons.push(pkmn)
    }
  },
  computed: {
    //propiedad computada que retorna cifra de pokemones seleccionados
    pokemonAmount() {
      return this.pokemons.length
    }
  }
}
</script>

<template>
  <!--componente header con contador de pokemones descubiertos, se asigna propiedad pokeCounter a pokemonAmount-->
  <HeaderComponent :pokeCounter="pokemonAmount" />
  <div class="row">
    <!--se itera por todos los pokemones para mostrar componente pokemon, con evento personalizado adddiscoveredpokemon-->
    <div v-for="(pokemon, id) in pokeData" :key="id" class="pokemon">
      <PokemonComponent :pokemon="pokemon" @add-discoveredPokemon="addDiscoveredPokemon" />
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
