<template>
    <div id="auxiliar">
    </div>
        <div class="card" id="container-poke">
        <div class="card-image">
            <figure id="imagempoke">
            <img :src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            
            <div class="media-content">
                <p class="title is-4">{{ num }} - {{ name.toUpperCase() }}</p>
                <div id="stats-left" >
                    <p id="fontepoke">{{ pokemon.type.toUpperCase() }}</p>
                    <p id="fontepoke">N° Pokedex: {{ pokemon.num }}</p>
                    <p id="fontepoke">HP: {{ pokemon.hp }}</p>
                    <p id="fontepoke">Ataque: {{ pokemon.attack }}</p>
                </div>
                <div id="stats-right">
                    <p id="fontepoke">Defesa: {{ pokemon.defense }}</p>
                    <p id="fontepoke">Ataque Especial: {{ pokemon.specialAttack }}</p>
                    <p id="fontepoke">Defesa Especial: {{ pokemon.specialDefense }}</p>
                    <p id="fontepoke">Velocidade: {{ pokemon.speed }}</p>
                </div>
            </div>
            </div>
            <div class="container-button">
                <button id="btnGirar" @click="girarPoke">Girar</button>
            </div>
        </div>
        </div>
</template>

<script>

import axios from 'axios'
export default {
    created: function(){
        //Fazendo a requisição usando a url de cada pokemon, resgatando todos os seus dados e suas sprites
        axios.get(this.url).then(res => {
            this.pokemon.hp = res.data.stats[0].base_stat;
            this.pokemon.attack = res.data.stats[1].base_stat;
            this.pokemon.defense = res.data.stats[2].base_stat;
            this.pokemon.specialAttack = res.data.stats[3].base_stat;
            this.pokemon.specialDefense = res.data.stats[4].base_stat;
            this.pokemon.speed = res.data.stats[5].base_stat;
            /*var id = res.data.id;
            var req = 'https://pokeapi.co/api/v2/evolution-chain/{'+{id}+'}/';
            this.pokemon.chain = axios.get(req);*/
            this.pokemon.num = res.data.id;
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
        })
    },
    data(){
        //Inicializando os dados que serão colocados em cada card
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                front: '', 
                back: ''
            }
        }
    },
    //Propriedades de um componente Poke
    props: {
        num: Number,
        name: String,
        url: String
    },
    //Criando método para girar a sprite do pokemon
    methods:{
        girarPoke: function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }else{
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style>
#auxiliar {
    margin-top:3%; 
}

#container-poke{
    width: 500px;
}

#btnGirar{
    width: 6rem;
    background-color: rgb(35, 106, 238);
    color: black;
    font-size: large;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    height: 3rem;
    border-radius: 1rem;
}

#imagempoke img{
    width: 180px;
}

#stats-left {
    width: 50%;
    float: left;
    text-align: left;
}
#stats-right {
    width: 50%;
    float: right;
    text-align: left;
}
#textopoke{
    font-size: medium;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
}

#fontepoke{
    font-weight: bold;
}

#container-button{
    align-items: center;
}
</style>