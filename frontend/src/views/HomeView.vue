<script setup lang="ts">
import { onMounted, reactive, ref } from 'vue';
interface PokemonInterface{
  name:string
}
let pokemons = reactive(ref<PokemonInterface[]>());

onMounted(()=>{
  // requisição do api

fetch("https://pokeapi.co/api/v2/pokemon?limit=1302&offset=0")
.then(res=>res.json())
.then(res=>pokemons.value=res.results);

})


</script>

<template>

      <main>
 <div class="container">
  <div class="row mt-4">
    <div class="col-sm-12 col-md-6">
      <div class="card" style="width: 18rem;">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg" class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
   
  </div>
</div>
<div class="col-sm-12 col-md-6">
  <div class="card" style="width: 18rem;">
<ul>
  <li v-for="pokemon in   pokemons" :key="pokemon.name">
{{ pokemon.name }}
  </li>

</ul>


  </div>
</div>


    </div>
  </div>
 </div>

  </main>


</template>
