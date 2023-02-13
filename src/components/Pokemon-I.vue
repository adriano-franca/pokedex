<template>
    <div id="pokemon">
    </div>
        <div class="card">
        <div class="card-image">
            <figure>
            <img :src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            
            <div class="media-content">
                <p class="title is-4">{{ num }} - {{ name.toUpperCase() }}</p>
                <div id="stats-left" >
                    <p class="subtitle is-7">{{ pokemon.type.toUpperCase() }}</p>
                    <p class="subtitle is-7">N° Pokedex: {{ pokemon.num }}</p>
                    <p class="subtitle is-7">HP: {{ pokemon.hp }}</p>
                    <p class="subtitle is-7">Attack: {{ pokemon.attack }}</p>
                </div>
                <div id="stats-right">
                    <p class="subtitle is-7">Defense: {{ pokemon.defense }}</p>
                    <p class="subtitle is-7">Special Attack: {{ pokemon.specialAttack }}</p>
                    <p class="subtitle is-7">Special Defense: {{ pokemon.specialDefense }}</p>
                    <p class="subtitle is-7">Speed: {{ pokemon.speed }}</p>
                </div>
            </div>
            </div>
            <div class="content">
                <button id="btnGirar" class="button is-fullwidth" @click="girarPoke">Girar</button>
            </div>
        </div>
        </div>
</template>

<script>

import axios from 'axios'
export default {
    created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.hp = res.data.stats[0].base_stat;
            this.pokemon.attack = res.data.stats[1].base_stat;
            this.pokemon.defense = res.data.stats[2].base_stat;
            this.pokemon.specialAttack = res.data.stats[3].base_stat;
            this.pokemon.specialDefense = res.data.stats[4].base_stat;
            this.pokemon.speed = res.data.stats[5].base_stat;
            this.pokemon.num = res.data.id;
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
        })
    },
    data(){
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
    props: {
        num: Number,
        name: String,
        url: String
    },
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
#pokemon {
    margin-top:3%;
}
#btnGirar{
    background-color: cornflowerblue;
    color: black;
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
</style>