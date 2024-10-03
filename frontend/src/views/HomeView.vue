<script setup>
import { onMounted, reactive, ref, computed  } from 'vue';
import ListPokemon from '../components/ListPokemon.vue';
//import CardPokemon from '../components/CardPokemon.vue';

let urlSvg=ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/")

let pokemons = reactive(ref());
// pesquisar 
let searchPokemonField= ref("")
let pokemonSelected = reactive(ref());
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

const selectPokemon = async(pokemon)=>{
  await fetch(pokemon.url)
.then(res=>res.json())
.then(res=> pokemonSelected.value=res);

console.log(pokemonSelected.value)
}

</script>

<template>

      <main>
 <div class="container text-body-secondary">

  <div class="row mt-4">
       <!-- busca -->
       <div class="mb-3">
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
    <div class="col-sm-12 col-md-6 ">
  
<!-- card detalhe -->

 <div class="card " >

    <img :src=" pokemonSelected?.sprites.other.dream_world.front_default"
      class="card-img-top pt-2" :alt="pokemonSelected?.name"
      height="120"
     > 
     <div class="card-body" v-if="pokemonSelected">
    <h5 class="card-title text-center text-capitalize fs-2 fw-700">{{pokemonSelected?.name}}</h5>
     
  
     <hr>
     
       <h3 class="mb-1 fs-2 fw-700 fst-italic text-decoration-underline"  
      style=" color: rgb(255,84,115);">Estatísticas</h3>
<div v-for="(stat,index) in pokemonSelected.stats " :key="index">
<span  class="d-flex justify-content-between flex-direction-row fs-4 lh-base ">{{ stat.stat.name }}
<strong>
  {{ stat.base_stat }}
</strong>  
</span>
</div>



<h3 class="mb-3 fs-2 fw-700 fst-italic text-decoration-underline
d-flex justify-content-center "  
style=" color: rgb(255,84,115);">Tipos</h3>

<ul class="list-group d-flex justify-content-center flex-row" >
  <li class="
  text-capitalize 
  badge text-body-secondary rounded-pill p-2 fs-5 bg-secondary-subtle " style="width: 25% ;margin-right: 10px;"
  v-for="(type,index) in pokemonSelected.types " :key="index">
    {{ type.type.name }}

  </li>
</ul>



</div>
</div> 




  <!-- <CardPokemon 
   
:name="pokemonSelected?.name"
:img="pokemonSelected?.sprites.other.dream_world.front_default"
:statname="pokemonSelected?.stat.name"
:basestat="pokemonSelected?.stat.base_stat"
/> -->





<!-- :nameesta="pokemonSelected?.stats.stat.name" -->
</div>
<div class="col-sm-12 col-md-6">
  <div class="card card-list" >
    <div class="card-body row">
 

      <ListPokemon
v-for="pokemon in pokemonsFilterd":key="pokemon.id"
:id="pokemon.id"
:name="pokemon.name"
:urlSvg="urlSvg + pokemon.url.split('/')[6]+'.svg'"
@click="selectPokemon(pokemon)"
/>

</div>


  </div>
</div>


    </div>
  </div>


  </main>


</template>
<style scoped>
.card-list{
  max-height: 450px;
overflow-y:scroll;
overflow-x: hidden;
}
@media (max-width: 768px) {
  .card-list{
    max-height: 48vh;
  }
}
</style>
