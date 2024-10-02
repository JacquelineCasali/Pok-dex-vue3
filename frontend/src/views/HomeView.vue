<script setup>
import { onMounted, reactive, ref, computed  } from 'vue';
import ListPokemon from '../components/ListPokemon.vue';

let urlSvg=ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/")

let pokemons = reactive(ref());
// pesquisar 
let searchPokemonField= ref("")
onMounted(()=>{
  // requisição do api

fetch("https://pokeapi.co/api/v2/pokemon?limit=1302&offset=0")
.then(res=>res.json())
.then(res=> pokemons.value=res.results
);

})
// filtro 
const pokemonsFilterd=computed (()=>{
  if(pokemons.value && searchPokemonField.value){
    return pokemons.value.filter(pokemon=>
      pokemon.name.toLowerCase().includes(searchPokemonField.value.toLowerCase())
    )
  }
  return pokemons.value
})

</script>

<template>

      <main>
 <div class="container">
  <div class="row mt-4">
  <!-- busca -->
<div class="mb-3" style="width: 80%;">
  <label 
                hidden 
                for="searchPokemonField" 
                class="form-label">
                Pesqiosar...
                </label>
  
  <input 
               v-model="searchPokemonField"
                type="text" 
                class="form-control" 
                id="searchPokemonField" 
                placeholder="Pesquisar...">
</div>
  
    <div class="col-sm-12 col-md-6 cards">
      <div class="card mx-4 " style="width: 18rem; height: 30rem;">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg" class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
   
  </div>
</div>
<div class="col-sm-12 col-md-6">
  <div class="card" >
    <div class="card-body row">



      <ListPokemon
v-for="pokemon in pokemonsFilterd":key="pokemon.name"
:name="pokemon.name"
:urlSvg="urlSvg + pokemon.url.split('/')[6]+'.svg'"

/>

</div>


  </div>
</div>


    </div>
  </div>
 </div>

  </main>


</template>
<style>
.cards{
  display: flex;
 width: 100%;
 justify-content: center
}
</style>
