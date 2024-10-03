<script setup>
import { onMounted, reactive, ref, computed  } from 'vue';
import ListPokemon from '../components/ListPokemon.vue';

let urlSvg=ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/")

let pokemons = reactive(ref());
// pesquisar 
let searchPokemonField= ref("")
let pokemonSelected = reactive(ref());

// carregamento de pagina 
let loading=ref(false)
onMounted(()=>{
  // requisição do api
fetch(`https://pokeapi.co/api/v2/pokemon?limit=1302&offset=0`)
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
// clica no card
const selectPokemon = async(pokemon)=>{
  loading.value=true;
  await fetch(pokemon.url)
.then(res=>res.json())
.then(res=> pokemonSelected.value=res)
.catch(err=>alert(err))
.finally(()=>loading.value.false)
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

 <div  class="card CardPokemonSelected " 
 :class=" loading ? '':'animate__animated animate__flipIny'" >
  


    <img
    v-if="pokemonSelected?.name"
    :src=" pokemonSelected?.sprites.other.dream_world.front_default"
      class="card-img-top pt-2" :alt="pokemonSelected?.name"
      height="95"
     > 
     <img 
     v-else
     src="../assets/pokemon.svg"
      class="card-img-top pt-2" alt="???"
      height="250"
     > 
     <div class="card-body" v-if="pokemonSelected">
   
   <div>

    <h5 class=" text-center text-capitalize fs-2 fw-700">{{pokemonSelected?.name }}</h5>
    <ul class="list-group d-flex justify-content-center flex-row" >
  <li class="
  text-capitalize 
  badge text-body-secondary rounded-pill p-2 fs-5 bg-secondary-subtle " style="width: 25% ;margin-right: 10px;"
  v-for="(type,index) in pokemonSelected.types " :key="index">
    {{ type.type.name }}

  </li>
</ul>
   </div>
     
  
    
     
 <h3 class="mb-1 fs-2 fw-700 fst-italic text-decoration-underline"  
      style=" color: rgb(255,84,115);">Estatísticas</h3>
<div v-for="(stat,index) in pokemonSelected.stats " :key="index"
class="d-flex justify-content-between flex-direction-row fs-4 lh-base ">
<span >{{ stat.stat.name }}
 </span>
<strong>
  {{ stat.base_stat }}
</strong> 
</div>

</div>
</div> 

</div>
<div class="col-sm-12 col-md-6">
  <div class="card card-list" >
    <div class="card-body row">
 

      <ListPokemon
v-for="pokemon in pokemonsFilterd":key="pokemon.name"
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

.CardPokemonSelected{
   height: 70vh;
   background: rgb(72,63,251);
   background: radial-gradient(circle, rgba(220, 194, 106, 0.8) 0%, rgba(244, 0, 0, 0.8) 100%);
}
.card-list{
  max-height: 70vh;
overflow-y:scroll;
overflow-x: hidden;
}


/* .CardPokemonSelected img{
    height: 250px;
} */
@media (max-width: 768px) {
  .card-list{
    max-height: 48vh;
  }

  .CardPokemonSelected{
        height: 68vh;
        width: 100%;
        margin: 0 auto 10px auto;
    }
    .CardPokemonSelected img{
        height: 100px;
    }
}
</style>
