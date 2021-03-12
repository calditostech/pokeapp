<template>
   <div id="pokemon">
       <div class="w3-container">
          <h2>Pokemon Card</h2>
  <div class="w3-card-4" style="width:50%">
    <img :src="pokemon.front" class="poke" alt="Placeholder imagem">
    <div class="w3-container w3-center">
        <div class="texto">
      <p>{{num}} - {{name | upper}}</p>
      <p>{{pokemon.type}}</p>
        </div>
    </div>
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
    }
}
</script>

<style>
    #pokemon{
        margin-top: 2%;
    }

    body {
        background-color: #f44336;
    }

    .w3-container{
        background-color: white;      
    }

    .texto{
        margin-left: 310px;
    }

    .poke{
        margin-left: 300px;
    }


</style>