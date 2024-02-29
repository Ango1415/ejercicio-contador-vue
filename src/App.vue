<!--SFC Single File Components : Todo los componentes en un mismo script-->
<script setup>
import{ref, computed} from 'vue'

let contador = ref(0)
let numFavoritos = ref([])
let isActiveAdd = ref(true)

const reiniciar= () => contador.value = 0

const verificarAñadir = () => { 
  const encontrado = numFavoritos.value.find((numero)=>contador.value === numero)
  if((encontrado !== undefined)){
    isActiveAdd.value = false
  }else{
    isActiveAdd.value = true
  }
}

const aumentar= () => {
  contador.value++
  verificarAñadir()
}

const disminuir= () => { 
contador.value--
verificarAñadir()
}

const añadirNumero = () => {
  numFavoritos.value.push(contador.value)
  verificarAñadir()
}

const eliminarNumero = () => {
  let indice = numFavoritos.value.findIndex((numero)=>contador.value === numero)
  if((indice !== undefined) ||(indice !== NaN)) numFavoritos.value.splice(indice, 1);
  verificarAñadir()
}

const colorContador = computed(() => { 
  if(contador.value === 0){
    return 'zero'
  }else if(contador.value > 0){
    return 'positive'
  }else {
    return 'negative'
  }
})

</script>

<template>
    <div class="container text-center mt-5">
        <h1>Ejercicio contador y números favoritos</h1><br>
        <h2 :class="colorContador">Valor del contador: {{ contador }}</h2><br>
        <div class="btn-group">
            <button @click="aumentar" class="btn btn-success">Aumentar</button>
            <button @click="disminuir" class="btn btn-danger">Disminuir</button>
            <button @click="reiniciar" class="btn btn-secondary">Reiniciar</button>
            <button @click="añadirNumero" :disabled="!isActiveAdd" class="btn btn-primary">Añadir</button>
            <button @click="eliminarNumero" :disabled="isActiveAdd" class="btn btn-primary">Eliminar</button>
        </div>
        <br>
        <br>
        <h2 class="mt33">Mis Favoritos</h2>
        <ul class="list-group mt-2">
            <li 
                class="list-group-item"
                v-for="(numero, index) in numFavoritos"  
                :key="index">
                    {{ numero }}
            </li>
        </ul>
    </div>
  
</template>

<style>
h1{
  color: crimson;
  text-align: center;
  font-weight: bolder;
}

.positive{
  color: green;
}

.negative{
  color: red;
}

.blue{
  color: blue;
}

.zero{
  color: inherit;
}
</style>