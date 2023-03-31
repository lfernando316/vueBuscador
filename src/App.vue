<template>
  <h2>Cena {{ contador + 1 }} con el rey godo {{ rey }}</h2>
  <h3 class="precio">Precio ${{ productos[contador].precio }}</h3>
  <div class="dias soloFinesDeSemana" v-if="productos[contador].finDeSemana">(Solo fines de semana)</div>
  <div v-else class="dias todosLosDias">(de lunes a domingo)</div>
  <img :src="imagen" alt="">
  <button @:click="siguiente">Siguiente ({{ contador + 1 }} / {{ total }})</button>
</template>
<script setup>
import { ref, computed } from "vue"
import { productos } from "./datos.js"
const contador = ref(0)
const total = productos.length;
const ruta = "https://www.html6.es/img/rey_"
const siguiente = () => {
  contador.value++
  if (contador.value >= total) {
    contador.value = 0
  }
}

const rey = computed(() => {
  const elNOmbre = productos[contador.value].nombre.toLowerCase()
  return elNOmbre.substring(0, 1).toUpperCase() + elNOmbre.substring(1)
})
const imagen = computed(() => {
  return `${ruta}${productos[contador.value].nombre.toLowerCase()}.png`
})
</script>

<style scoped>
.todosLosDias {
  background-color: green
}

.soloFinesDeSemana {
  background-color: red;
}

.dias {
  color: white;
  padding: 4px 17px;
  font-size: 0.9em;
  border-radius: 4px;
  margin: 5px 0 10px;
  display: inline-block;
}
</style>