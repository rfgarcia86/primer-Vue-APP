<script setup>
import { ref, computed, reactive } from 'vue';

const arregloNumeros = ref([]);
const numero = ref(0);

const incrementar = () => numero.value ++;
const decrementar = () => numero.value --;
const resetear = ()=> {
  numero.value = 0;  

  while(arregloNumeros.value.length > 0){  
    let elemento = arregloNumeros.value.pop();    
  }   
};

const agregar = () =>{
  arregloNumeros.value.push(numero.value);  
}

const repetido = computed(()=>{
  return arregloNumeros.value.some((item)=> item === numero.value);  
});
// igual con menos codigo
// const repetido = computed(()=> arregloNumeros.value.some((item)=> item === numero.value));  

const vacio = computed(()=>{
  return arregloNumeros.value.length === 0 ? true : false;
});
// igual con menos codigo
// const vacio = computed(()=>arregloNumeros.value.length===0?true:false);

const colorNumero = computed(()=>{
  if(numero.value === 0) return 'text-info';  
  return numero.value > 0 ? 'text-success' : 'text-danger';
});


</script>

<template> 
  <div class="container text-center mt-5">
    <h1>{{arregloNumeros}}</h1>
    
    <h2 :class="colorNumero">{{numero}}</h2> 
    <div class="btn-group">
      <button class="btn btn-success" @click="incrementar">Incrementar</button>
      <button class="btn btn-danger" @click="decrementar">Decrementar</button>
      <button class="btn btn-primary" @click="agregar" :disabled="repetido">Agregar</button>
      <button class="btn btn-secondary" @click="resetear" :disabled="vacio">Resetear</button>
    </div>
    <br/>
    <ul class="list-group mt-2">
      <li class="list-group-item" v-for="(item,index) in arregloNumeros" :key="index">      
        {{item}}                          
      </li>  
    </ul>
  </div>
</template>

<style>
.positivo{
  color: green;
}
.negativo{
  color: red;
}
.zero{
  color: peru;
}
</style>