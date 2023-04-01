<template>
  <div id="app">
    
    
    <div class="column is-half is-offset-one-quarter">
      <input type="text" class="input is-rounded" name="" id="" placeholder="Buscar Pokémon pelo nome" v-model="busca">
      <button id="buscaBtn" class="button is-medium is-success" @click="buscar">Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <MyPokemon :name ="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
    
  </div>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>

import axios from 'axios';
import MyPokemon from './components/MyPokemon';
export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },

  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Pegou a lista de pokemon!");
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  components: {
    MyPokemon
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ''){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }
  },
  computed: {
   /* resultadoBusca: function(){
      if(this.busca == '' || this.busca == ''){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }*/
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

#buscaBtn{
  margin-top: 2%;
}
</style>
