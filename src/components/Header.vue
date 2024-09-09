<script>
export default {
  name: 'HeaderComponent',
  //se establece propiedad pokeCounter para mostrar contador en template
  props: {
    pokeCounter: {
      type: Number,
      required: true
    }
  }
}
</script>

<template>
  <figure><img src="@/assets/pokemon.png" alt="Pokemon Logo" /></figure>
  <br />
  <h1>¿Quién es ese Pokémon?</h1>
  <div>
    <p>Introduce el nombre del Pokemon bajo su silueta para revelarlo si aciertas.</p>
    <h2>
      Pokemones descubiertos: <span>{{ pokeCounter }}</span>
    </h2>
  </div>
</template>

<style scoped>
h1,
p,
h2 {
  text-align: center;
}
figure {
  display: flex;
  justify-content: center;
}
h1,
h2 {
  font-weight: bold;
}
span {
  color: sandybrown;
}
</style>
