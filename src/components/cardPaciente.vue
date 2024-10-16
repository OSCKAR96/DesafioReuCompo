<template>
  <div class="cardPac">
    <h4>Nombre Paciente: {{ nombre }}</h4>
    <h4>Fecha: {{ fecha }}</h4>
    <h4>Hora: {{ hora }}</h4>
    <h4>Motivo: {{ motivo }}</h4>
    <button class="textoRojo" @click="$emit('eliminarPaciente')">Cancelar</button>
  </div>
</template>

<script>
export default {
  name: "cardPaciente",
  props: {
    nombre: String,
    fecha: String,
    hora: String,
    motivo: String,
  },
};
</script>

<style scoped>
.cardPac{
    margin: 30px;
}
.textoRojo{
background-color: black;
color: white;
}
</style>
