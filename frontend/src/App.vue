 <template>

 
<nav class="navbar navbar-expand-lg navbar-dark bg-primary">
  <div class="container-fluid">
    <router-link  class="navbar-brand" to="/">
      <img src="./assets/icon.svg" alt="Logo" width="30" height="24" class="d-inline-block align-text-top">
      Pokédex
    </router-link >
    
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <router-link  class="nav-link " aria-current="page" to="/">Home</router-link >
        </li>
        <li class="nav-item">
          <router-link  class="nav-link" to="/about">About</router-link >
        </li>
     
      </ul>
    
    </div>
    <Dark />
  </div>

</nav>
<div class="main">
    <router-view></router-view>
  </div>


<footer class="bg-primary text-light">
  <div>Desenvolvido por Jacqueline Casali</div>
</footer>

</template>

<script  lang="ts">
import Dark from './components/Dark.vue';
export default {
  // name:"App",
  components:{
    Dark,
  }
}




// defineProps<{
//   msg: string,
//   Date:Date
// }>()

</script>

<style>
footer{
  position: fixed;
  bottom: 0;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 56px;
}
</style>







