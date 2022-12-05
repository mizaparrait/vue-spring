<template>
  <div class="home center">
    <form class="container">
      <label for="name">Escribe tu nombre</label>
      <input id="name" type="text" placeholder="nombre" v-model="name" />
      <button type="submit" @click="handleSubmit">Submit</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";
import PersonaService from "../Service/PersonaService";

const personaService = new PersonaService

const name = ref("");

// eslint-disable-next-line no-unused-vars
const handleSubmit = (event) => {
  event.preventDefault();
  console.log("enviado", name.value);
  const persona = {"id": 2, "nombre": name.value}//Para la funcion save()
  personaService.getAll().then(data => {

    const elementos = data

    console.log(elementos.data[0].nombre)//Asi se accede a la propiedad nombre.
  })//Aqui se va imprimir en pantalla y no en consola

  personaService.save(persona).then(data => {
      console.log(data)
    })
};
</script>

<style scoped>
.center {
  display: flex;
  justify-content: center;
}
.container {
  display: flex;
  flex-direction: column;
  width: fit-content;
}
</style>
