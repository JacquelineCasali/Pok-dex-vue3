<script setup>
import {useDark , useToggle} from '@vueuse/core'
const isDark=useDark({
    // onChanged(isDark){
    //     if(isDark){
    //         document.documentElement.classList.add('dark')
    //     }else{
    //         document.documentElement.classList.remove('dark')
    //     }
    // }
    // selector:'body',
    // attribute:'color-scheme',
    // valueDark:'custom-dark',
    // valueLight:'custom-light'
});
const toggleDark=useToggle(isDark);

</script>
<template>
    <button 
    @click="toggleDark()"
    class="px-4 py-2 bg-green-500 text-white  rounded dark:bg-purple-500"
    >Dark Mode</button>
    </template>