<template>
    <button @click="myNumber++">click me</button>
    <p>clicked {{ myNumber }} times</p>
</template>

<script setup>
 
import { ref } from 'vue'

const myNumber = ref(0)


function clickedBtn(){
    ref ++;
}
</script>
