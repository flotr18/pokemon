<template>
  <div id="app">
  {{ dada }}
  <main_pokemon></main_pokemon>
  </div>
</template>

<script>
import axios from "axios"
import main_pokemon from './components/Main_Pokemon.vue'

export default {
  name: 'App',
  components: {
    main_pokemon
  },
  data () {
    return {
      dada: null
    }
  },
  mounted() {
    axios
      .get('https://pokeapi.co/api/v2/pokemon/1')
      .then(response => (this.dada = response.data.abilities[0].ability.name))
      .catch(error => console.log(error))

  }
}
</script>

<style>

@font-face {
  font-family: "Pokemon_font";
  src: local("Pokemon_font"),
      url("assets/Pokemon Solid.ttf");
}

#app {
  font-family: Pokemon_font,serif;
}

</style>
