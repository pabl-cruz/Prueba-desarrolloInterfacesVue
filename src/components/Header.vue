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
  <figure><img src="/pokemon-logo.svg" alt="Pokemon Logo" /></figure>
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
h1 {
  font-size: 40px;
  margin-bottom: 0.5rem;
}

p {
  font-size: 16px;
}

h2 {
  font-size: 28px;
  margin: 2rem auto;
  background-color: #2ad2eb;
  color: #fff;
  width: max-content;
  padding: 2rem;
  border-radius: 80px;
  text-shadow: 1px 1px 2px #00000096;
}

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
  color: #9f09a7;
  margin-left: 0.5rem;
}

img {
  width: 33%;
}
</style>
