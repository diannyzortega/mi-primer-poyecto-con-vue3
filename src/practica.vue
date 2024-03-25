<script setup>
import { ref, computed } from 'vue'

const name = 'Vue Dinamico'
const styleColor="color:blue"
const arrayColores= ["blue","red","yelow"]
const activo= true
const arrayFrutas= ['🍉','🍓','🍒','🌽','🍅','🥑']
const arrayFrutas2 =[
  {
    name: "manzana",
    price: "1$",
    description: "una manzana"

  },
  {
    name: "pera",
    price: "2$",
    description: "una pera"

  },
  {
    name: "naranja",
    price: "3$",
    description: "una naranja"

  }
]
const objetoFruta =  {
    name: "manzana",
    price: "1$",
    description: "una manzana"

  }
  const arrayFrutas3 =[
  {
    name: "manzana",
    price: "1$",
    description: "una manzana",
    stock: "0"

  },
  {
    name: "pera",
    price: "2$",
    description: "una pera",
    stock: "10"

  },
  {
    name: "naranja",
    price: "3$",
    description: "una naranja",
    stock: "20"

  }
]

//metodo para activar button
const handleClick= () => {
  console.log('me diste click')
}
//metodo para activar button
const handleClick2= (message) => {
  console.log(message)
}
//metodo para activar button
const handleClick3= (message) => {
  console.log(message)
}

const counter = ref(0) 

const increment = () => {
  counter.value++;
}
const disminuir = () => {
  counter.value--;
}
const resetear = () => {
  counter.value = 0;
}
const cambioColor= (value) => {
  if (counter.value > 0) {
    return "color:green"
  }
  if (counter.value < 0) {
      return "color:red"
  } else {
    return "color:none"
  }
}

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
<h1>Hola {{ name.toLocaleUpperCase() }}</h1>
  <h2>{{ arrayColores }}</h2>
  <h2 :style=styleColor>Soy azul</h2>
  <h2 :style="`color: ${arrayColores[1]}`">No soy azul</h2>
  <h2>{{activo ? "Estoy Activo": "Estoy Inactivo"}}</h2>
  <p v-if="activo">Estoy Activo</p>
  <p v-if="!activo">Estoy Inactivo</p>
  <p v-if="activo">Estoy Activo</p>
  <p v-else>Estoy Inactivo</p>
  <h2 v-show="activo">Estoy activo v-show</h2>

  <ul>
    <li v-for="(fruta, index) in arrayFrutas":key="index"> {{ index + 1 }} - {{fruta}} </li>
  </ul>
  <ul>
    <li v-for="(fruta2) in arrayFrutas2":key="fruta2.name">
     {{fruta2.name}} - {{ fruta2.price }} - {{ fruta2.description }} </li>
  </ul>
  {{ objetoFruta }}
  <ul>
    <li v-for="(value, propiedad, index) in objetoFruta":key="index">{{ index + 1 }} - {{ propiedad }} : {{ value }}</li>
  </ul>
  <ul>
    <template v-for="item in arrayFrutas3":key="item.name">
      <li v-if="item.stock > 0">
   {{ item.name }} - {{ item.price }}</li>
    </template>    
  </ul>
  <button v-on:click="handleClick">Activame 1</button>
  <button @click="handleClick">Activame 2</button>
  <button v-on:click="handleClick2('Texto 1')">Activame</button>
  <button @click="handleClick2('Texto 2')">Activame</button>
  <button v-on:click.right.prevent="handleClick3('Texto right')">Activame right</button>
  <button @click="handleClick3('Texto left')">Activame left</button>
  <button @click.middle="handleClick3('Texto middle')">Activame middle</button>
  <button ref="counte.value" @click="increment()">Aumentar</button>
  <h2>{{ counter }}</h2>


  <button ref="counter.value" @click="counter++">Aumentar</button>
  <button ref="counter.value" @click="disminuir()">Disminuir</button>
  <button ref="counter.value" @click="resetear()">Resetear</button>
  <h2 :style="cambioColor(counter.value)">{{ counter }}</h2>
  <h2 :class="counter > 0 ? 'positive' : 'negative'">{{ counter }}</h2>
  <h2 :class="classCounter">{{ counter }}</h2>
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