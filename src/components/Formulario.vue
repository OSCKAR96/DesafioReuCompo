<template>
  <div>
    <form @submit.prevent="agregarPaciente">
      <h1>Este es un titulo</h1>
      <div>
        <label
          for="paciente"
          class="form-label"
          :class="{ incompleto: !datosPaciente.nombre }"
          >Paciente</label
        >
        <input
          type="text"
          name="nombre"
          class="form-control"
          id="nombre"
          v-model="datosPaciente.nombre"
        />
      </div>

      <div>
        <label
          for="fecha"
          class="form-label"
          :class="{ incompleto: !datosPaciente.fecha }"
          >Fecha</label
        >
        <input
          type="date"
          name="fecha"
          class="form-control"
          id="fecha"
          v-model="datosPaciente.fecha"
        />
      </div>

      <div>
        <label
          for="hora"
          class="form-label"
          :class="{ incompleto: !datosPaciente.hora }"
          >Hora</label
        >
        <input
          type="time"
          name="hora"
          class="form-control"
          id="hora"
          v-model="datosPaciente.hora"
        />
      </div>

      <div>
        <label
          for="gravedad"
          class="form-label"
          :class="{ incompleto: !datosPaciente.gravedad }"
          >Gravedad</label
        >
        <select
          name="gravedad"
          class="form"
          id="gravedad"
          v-model="datosPaciente.gravedad"
        >
          <option v-for="(gravedad, index) in nivelGravedad" :key="index">
            {{ gravedad }}
          </option>
        </select>
      </div>

      <div>
        <label
          for="motivo"
          class="form-label"
          :class="{ incompleto: !datosPaciente.motivo }"
          >Motivo</label
        >
        <input
          type="text"
          name="motivo"
          class="form-control"
          id="motivo"
          v-model="datosPaciente.motivo"
        />
      </div>

      <div>
        <button class="mt-5" :disabled="!formularioCompleto">agregar</button>
      </div>
    </form>
    <section>
      <p class="textoRojo" v-if="listaPacientes.length < 1">
        No se han registrado consultas.
      </p>
      <div>
        <cardPaciente
          v-for="(paciente, index) in listaPacientes"
          :key="index"
          :style="colorCard(paciente.gravedad)"
          :nombre="paciente.nombre"
          :fecha="paciente.fecha"
          :hora="paciente.hora"
          :motivo="paciente.motivo"
          @eliminarPaciente="listaPacientes.splice(index, 1)"
        />
      </div>
    </section>
  </div>
</template>

<script>
import cardPaciente from "./cardPaciente.vue";

export default {
  name: "Formulario",
  components: {
    cardPaciente,
  },
  data() {
    return {
      nivelGravedad: ["Baja", "Media", "Alta"],
      datosPaciente: {
        nombre: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      },
      listaPacientes: [],
    };
  },
  methods: {
    agregarPaciente() {
      const nuevoPaciente = { ...this.datosPaciente };
      this.listaPacientes.push(nuevoPaciente);
      this.limpiarCampos();
    },

    limpiarCampos(){
      this.datosPaciente = {
        nombre: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      };
    },
    colorCard: function (gravedad){
      if(gravedad == "Baja"){
        return "backgroundColor: Green;";
      } else if( gravedad =="Media"){
        return "backgroundColor: Yellow;";
      } else if( gravedad == "Alta"){
        return "backgroundColor: Red;"
      }
    }
  },

  computed: {
    formularioCompleto() {
      return (
        this.datosPaciente.nombre &&
        this.datosPaciente.fecha &&
        this.datosPaciente.hora &&
        this.datosPaciente.gravedad &&
        this.datosPaciente.motivo
      );
    },
  },
};
</script>

<style scoped>
.incompleto {
  color: red;
}
</style>
