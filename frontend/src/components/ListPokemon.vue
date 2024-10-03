<script setup lang="ts">
const pokemon =defineProps(["name","urlSvg","id"])

</script>

<template>
<div class="col-4 ">
  <div  class="card p-2 mb-4 cardListPokemon">
    <p>{{ pokemon.id }}</p>
    <p class="text-center text-capitalize fs-5 fw-bold">{{pokemon.name}}</p>
    <img :src="urlSvg" class="card-img-top" alt="..."
    height="80">
  </div>

</div>
</template>

<style scoped>
.cardListPokemon{
    background: rgb(72,63,251);
    background: radial-gradient(circle, rgba(94, 87, 232, 0.5) 0%, rgba(70,252,244,0.5) 100%);
    cursor: pointer;
}
.cardListPokemon:hover{
    background: rgb(72,63,251);
    background: radial-gradient(circle, rgba(72,63,251,0.6) 0%, rgba(70,252,244,0.4) 100%);
}
.cardListPokemon img:hover{
    padding: .5rem;
}
</style>