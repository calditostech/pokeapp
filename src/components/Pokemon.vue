<template>
     <div id="pokemon">
     <div class="w3-container">
          <h2>Pokemon Card</h2>
      <div class="w3-card-4" style="width:50%">
           <img :src="pokemon.front" alt="Placeholder imagem">
      <div class="w3-container w3-center">
           <p>{{num}} - {{name | upper}}</p>
           <p>{{pokemon.type}}</p>
      </div>
      </div>
      <div class="content">
            <button class="button is-medium is fullwidth" @click="exibirValores">Caracteristicas</button>
      </div>
   </div>
   </div>
</template>

<script>
import axios from 'axios';
export default {
    created: function(){
        axios.get(this.url).then(res => {
           this.pokemon.type = res.data.types[0].type.name;
           this.pokemon.front = res.data.sprites.front_default;
           this.pokemon.back = res.data.sprites.back_default;
           console.log(this.pokemon);
        })
    },
    data(){
        return {
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
    filters: {
        upper: function(value){
            var newName = value[0].toUpperCase() + value.slice(1);
            return newName;
        }
    },
    methods: {
        exibirValores: function(){

        }
    }
}
</script>

<style>
    #pokemon{
        margin-top: 2%;
    }
</style>