
<script setup lang="ts">

// import Dark from "./components/Dark.vue";
import Dark from "./components/Dark.vue";
import {ref} from 'vue';

let num=ref(0)
// defineProps<{
//   msg: string
// }>()
</script>


 
 <template>
<Dark/>
<div>
  <button @click="num++">{{ num }}</button>
</div>
</template>
<style>
html.dark{
  color-scheme: dark;
}
body{
 @apply bg-slate-50 text-slate-800 dark:bg-slate-800 dark:text-slate-50
}
</style>







