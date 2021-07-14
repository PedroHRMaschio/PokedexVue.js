<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokemon.png" alt="">
      <p class="title is-2 is-spaced">Pokedéx</p>
      <div class="box">
        <input type="text" name="" class="input is-normal" id="" placeholder="Busca pelo nome" v-model="busca">
        <button class="button is-fullwidth is-light" id="busca-btn" @click="buscar">Realizar busca</button>
      </div>
      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
        <pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";
export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ""
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Lista de pokemons adquirida")
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    });
  },
  components: {
    Pokemon
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == "" || this.busca == " "){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(poke => poke.name == this.busca);
      }
    }
  },
  computed: {
    /*
    resultadoBusca: function(){
      if(this.busca == "" || this.busca == " "){
        return this.pokemons;                               Esse método é usado para realizar a busca sem o botão, em tempo real, utilizando mais poder computacional
      }else{
        return this.pokemons.filter(poke => poke.name == this.busca)
      }
    }
    */
  }
}
</script>

<style>
#app{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 1%;
  background-color: lightskyblue;
}
#busca-btn{
  margin-top: 1%;
}
</style>
