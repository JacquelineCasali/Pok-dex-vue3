<script setup lang="ts">

import {useDark , useToggle} from '@vueuse/core'
const isDark=useDark({
 
     selector:'body',
     attribute:'color-scheme',
    valueDark:'dark',
    valueLight:'light'
});
const toggleDark=useToggle(isDark);

</script>
<template>
 
 
    


 <label class="switch">
  <input type="checkbox"
   @click="toggleDark()"
  >
  <span class="slider round"></span>
</label>

    </template>
    <style>
    body{
        height: 100vh;
    }
/* The switch - the box around the slider */
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
  margin-right: 50px;
}

/* Hide default HTML checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

/* The slider */
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}

[color-scheme='dark']{
    background: rgb(106,196,233);
    background: linear-gradient(0deg, rgba(106,196,233,0.9360119047619048) 0%, rgba(0,41,150,1) 100%);

}
[color-scheme='light']{
    background-color:white;
}
</style>
