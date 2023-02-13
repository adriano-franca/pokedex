<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokemon.png">
      <hr>
      <h3 class="is-size-3">Pokedex</h3>
      <input type="text" class="input is-rounded" name="" id="" placeholder="Digite o nome do pokemon..." v-model="busca">
      <div>
        <button class="button" id="btnBusca" @click="buscar">Buscar</button>
        <button class="button" id="btnBusca" @click="withEvolutions">Buscar com evoluções</button>
      </div>
      <div v-for="(poke, index) in pokeFiltro" :key="poke.url">
      <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />
    </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios'
import Pokemon from './components/Pokemon-I'

export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      pokeFiltro: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Pokemons was caught");
      this.pokemons = res.data.results;
      this.pokeFiltro = res.data.results;
    })
  },
  components: {
    Pokemon, 
  },
  methods: {
    buscar: function(){
      this.pokeFiltro = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
        this.pokeFiltro = this.pokemons;
      }else{
        this.pokeFiltro = this.pokemons.filter(pokemon => pokemon.name.toUpperCase() == this.busca.toUpperCase())
      }
    },
    withEvolutions: function(){
      if(this.busca == '' || this.busca == ' '){
        this.pokeFiltro = this.pokemons;
      }else{
        alert("Ainda em desenvolvimento");
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#btnBusca {
  margin-top: 2%;
  size: 50%;
  background-color: rgb(0, 128, 0);
  color: white;
}
</style>
