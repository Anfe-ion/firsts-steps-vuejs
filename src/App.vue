<script setup>
import { ref, computed } from "vue";

const name = 'Dinamic Vue'
const style = 'font-size: 100px; font-weight: bold; color: pink'
const arrayColors = ['Hotpink', 'Turquoise', 'Gold']
const activo = false
const arrayFrutas = ["🍎", "🍌", "🍐", "🍉"]
const arrayObjetos =
  [
    {
      name: "Manzana",
      price: "$1.00",
      description: "Una manzana",
      stock: 0,
    },
    {
      name: "Pera",
      price: "$2.00",
      description: "Una pera",
      stock: 10,
    },
    {
      name: "Naranaja",
      price: "$3.00",
      description: "Una naranja",
      stock: 20,
    }
  ]
const arrayObjetosUnico =
{
  name: "Manzana",
  price: "$1.00",
  description: "Una manzana",
}
//Methods
const hadleClick = (message) => {
  console.log(message)
}

const counter = ref(0)
const arrayFavs = ref([]);

const increment = () => counter.value++;

const decrement = () => counter.value--;

const reset = () => counter.value = 0;

const add = () => {
  arrayFavs.value.push(counter.value)
}

const blockButton = computed(() => {
  if (arrayFavs.value.includes(counter.value)) {
    return true
  }
})

const classCounter = computed(() => {
  if (counter.value == 0) {
    return 'zero'
  } if (counter.value > 0) {
    return 'positive'
  } else {
    return 'negative'
  }
})


</script>

<template>

  <div>
    <h1>{{ name.toUpperCase() }}</h1>

    <!-- <p :style="style">Perrito</p> -->

    <p :style="`color: ${arrayColors[1]}`">Soy {{ arrayColors[1] }}</p>

    <p :style="{ color: activo ? 'green' : 'red' }">
      {{ activo ? "I'm Active" : "I'm not active" }}
    </p>

    <p v-if="activo">I'm Active</p>
    <p v-else>I'm not Active</p>

    {{ arrayFrutas }}

    <p v-for="(fruta, index) in arrayFrutas" v-bind:key="index">
      {{ index + 1 }} - {{ fruta }}
    </p>

    <p v-for="objeto in arrayObjetos" key="fruta.name">
      {{ objeto }}
    </p>

    <p v-for="objeto in arrayObjetos" key="fruta.name">
      {{ objeto.name }}
    </p>

    <p v-for="objeto in arrayObjetos" key="fruta.name">
      {{ objeto.price }}
    </p>

    <p v-for="objeto in arrayObjetos" key="fruta.name">
      {{ objeto.description }}
    </p>

    <p v-for="(objeto, index) in arrayObjetos" key="name">
      {{ index + 1 }}. {{ objeto.name }} que cuesta {{ objeto.price }} y es {{ objeto.description }}
    </p>

    <hr>
    <ul>
      <li v-for="(value, propiedad, index) in arrayObjetosUnico" :key="value.arrayObjetosUnico">
        {{ index + 1 }}. {{ propiedad }}: {{ value }}
      </li>
    </ul>

    <template v-for="item in arrayObjetos" :key="name.arrayObjetos">
      <li v-if="item.stock > 0">{{ item.name }}</li>
    </template>
  </div>

  <!-- Events -->
  <div>
    <button v-on:click="hadleClick('Active 1')">Active me</button>
    <button @click="hadleClick('Active 2')">Active me</button>
    <br>
    <button @click.left="hadleClick('Left Text')">Active me left</button>
    <button @click.middle.prevent="hadleClick('Middle Text')">Active me Middle</button>
    <button @click.right.prevent="hadleClick('Right Text')">Active me right</button>
  </div>

  <div>
    <button @click="increment">Aumentar</button>
    <button @click="decrement">Decrementar</button>
    <button @click="reset">Reset</button>
    <button @click="add" :disabled="blockButton">Add to favorites</button>
    <p :class="classCounter"> {{ counter }}</p>
    <ul v-for="numeros in arrayFavs">
      <li>{{ numeros }}</li>
    </ul>
  </div>

</template>

<style>
h1 {
  color: blueviolet;
  font-weight: bold;
}

.zero {
  color: black;
  font-weight: bold;
}

.positive {
  color: greenyellow;
  font-weight: bold;
}

.negative {
  color: palevioletred;
  font-weight: bold;
}
</style>
