<script setup>
import { ref, computed } from 'vue'
const counter = ref(0) 
const arrayNumeros=ref([])

const name = 'Vue Dinamico'

const increment = () => {
  counter.value++;
}
const disminuir = () => {
  counter.value--;
}
const resetear = () => {
  counter.value = 0;
}
const add = (numero) => {

  arrayNumeros.value.push(numero)

}
const bloquearBtnAdd = computed(() =>{
  const numSearch = arrayNumeros.value.find(num => num === counter.value)
  if (numSearch === 0) return true;
  return numSearch ? true : false;
})
const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  }
  if (counter.value < 0) {
    return 'negative'
  }
})

</script>
<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toLocaleUpperCase() }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    
    <div class="btn-group">
      <button class="btn btn-success" ref="counter.value" @click="increment()">Aumentar</button>
      <button class="btn btn-danger" ref="counter.value" @click="disminuir()">Disminuir</button>
      <button class="btn btn-secondary" ref="counter.value" @click="resetear()">Resetear</button>
      <button class="btn btn-primary" ref="counter.value" @click="add(counter)" :disabled="bloquearBtnAdd">Add</button>
    </div>
    <ul class="list-group mt-4">
      <li  class="list-group-item" v-for="(numero, index) in arrayNumeros":key="index">
      {{numero}}</li>
    </ul>
  </div>
</template>

<style>
h1 { 
  color: red;
  }
.positive {
  color: green;
}
.negative {
  color: red;
}
.zero {
  color: peru;
}
</style>