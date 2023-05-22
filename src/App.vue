<template>
  <div class="app">
    <div class="container">
      <div class="container-img">
      <img id="imagem" src="./assets/pokemon.png">
      </div>
      <input type="text" class="input is-rounded" name="" id="barra-busca" placeholder="Digite o nome do pokemon..." v-model="busca">
      <div class="container-buttons">
        <button class="button" id="btnBusca" @click="buscar">Buscar</button>
        <button class="button" id="btnBusca" @click="withEvolutions">Buscar com evoluções</button>
      </div>
        <div class="container-poke" id="container-poke" v-for="(poke, index) in pokeFiltro" :key="poke.url">
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
      pokeChain: [],
      pokeChainFiltro: [],
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
    axios.get("https://pokeapi.co/api/v2/evolution-chain?limit=78&offset=0").then(res2 => {
      this.pokeChain = res2.data.results;
      this.pokeChainFiltro = res2.data.results;
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
        this.pokeFiltro = this.pokemons.filter(pokemon => pokemon.name.includes(this.busca))
      }
    },
    //Criando um método para retornar o pokemon que está no campo de busca e a sua cadeia de evolução, futuramente pretendia colocar tudo em um único botão
    withEvolutions: function(){
      if(this.busca == '' || this.busca == ' '){
        this.pokeChainFiltro = this.pokemons;
      }else{
        alert("nada")
      }
    }
  }
}
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  align-items: center;
}

.container{
  flex-direction: column;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container-poke{
  padding: 1%;
}

.container-img{
  padding: 10px
}

.container-buttons{
  padding: 10px;
}

#btnBusca {
  background-color: rgb(0, 128, 0);
  color: white;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  border-radius: 10px;
}

#barra-busca{
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  width: 50%;
}

#imagem{
  width: 300px;
}

</style>
