<template>
  <div class="app">
    <div class="container" id="container">
      <img id="imagem" src="./assets/pokemon.png">
      <h3 class="is-size-3">Pokedex</h3>
      <input type="text" class="input is-rounded" name="" id="barra-busca" placeholder="Digite o nome do pokemon..." v-model="busca">
      <div>
        <button class="button" id="btnBusca" @click="buscar">Buscar</button>
        <button class="button" id="btnBusca" @click="withEvolutions">Buscar com evoluções</button>
      </div>
        <div id="container-poke" v-for="(poke, index) in pokeFiltro" :key="poke.url">
          <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />
      </div>
    </div>
  </div>
</template>

<script>

//Import do axios e do componente que irá conter os pokemons
import axios from 'axios'
import Pokemon from './components/Pokemon-I'

export default {
  name: 'App',
  //Inicializando array de pokemons, o array que irá conter os pokemons filtrados e a variável que irá conter o que será preenchido no campo de busca
  data(){
    return{
      pokemons: [],
      pokeFiltro: [],
      busca: ''
    }
  },
  //Fazendo a requisição para a PokeAPI dos 151 pokemons da primeira geração
  //Resgatei apenas os 151 primeiros para a aplicação não ficar tão lenta
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
      this.pokeFiltro = res.data.results;
    })
  },
  //Colocando Pokemon como componente
  components: {
    Pokemon, 
  },
  methods: {
    //Criando os métodos de busca para buscar um específico
    buscar: function(){
      //Inicializa o array para filtro com todos os pokemons
      this.pokeFiltro = this.pokemons;
      //Se o campo de busca estiver vazio ele retorna todos os pokemons
      if(this.busca == '' || this.busca == ' '){
        this.pokeFiltro = this.pokemons;
      }else{
        //Filtrando os pokemons pelo nome, usei o uppercase para considerar igual independente da escrita, ou seja, BuLbAsAuR e bulbasaur seriam considerados iguais e retornariam o pokemon
        this.pokeFiltro = this.pokemons.filter(pokemon => pokemon.name.toUpperCase() == this.busca.toUpperCase())
      }
    },
    //Criando um método para retornar o pokemon que está no campo de busca e a sua cadeia de evolução, futuramente pretendia colocar tudo em um único botão
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
  text-align: center;
  margin-top: 30px;
  align-items: center;
}
#btnBusca {
  margin-top: 2%;
  size: 50%;
  background-color: rgb(0, 128, 0);
  color: white;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}

#barra-busca{
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}

#imagem{
  width: 300px;
}

#container{
  align-items: center;
}

</style>
