<template>
        <div class="card" id="container-poke">
        <div class="card-image">
            <figure class="imagempoke">
            <img :src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            
            <div class="media-content">
                <p class="title is-4">{{ pokemon.id }} - {{ name[0].toUpperCase()+name.slice(1) }}</p>
                <div id="stats-left" >
                    <p id="fontepoke">{{ pokemon.type.toUpperCase() }}</p>
                    <p id="fontepoke">Altura: {{ pokemon.height }}</p>
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
            this.pokemon.id = res.data.id;
            this.pokemon.height = res.data.height;
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
        id: Number,
        name: String,
        url: String,
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

#container-poke{
    width: 500px;
    border-radius: 20px;
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

.imagempoke img{
    width: 180px;
    border-top-right-radius: 20px;
    border-top-left-radius: 20px;
}

.card-content{
    background-color: rgb(211, 211, 211);;
    border-top-right-radius: 200px;
    border-top-left-radius: 20px;
}

.card{
    background-color: rgb(211, 211, 211);
    border-radius: 20px;
}

.card-image{
    border-top-right-radius: 20px;
    border-top-left-radius: 20px;
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