<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12">
        <h1>Personas</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <formulario-persona v-on:add-persona="agregarPersona"/>
        <tabla-personas
            v-bind:personas="personas"
            v-on:delete-persona="eliminarPersona"
            v-on:actualizar-persona="actualizarPersona"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TablaPersonas from '@/components/TablaPersonas.vue'
import FormularioPersona from "./components/FormularioPersona";

export default {
  name: 'App',
  components: {
    FormularioPersona,
    TablaPersonas
  },
  data() {
    return {
      personas: [
        {
          id: 1,
          nombre: 'Jon',
          apellido: 'Nieve',
          email: 'jon@email.com',
        },
        {
          id: 2,
          nombre: 'Tyrion',
          apellido: 'Lannister',
          email: 'tyrion@email.com',
        },
        {
          id: 3,
          nombre: 'Daenerys',
          apellido: 'Targaryen',
          email: 'daenerys@email.com',
        },
      ]
    }
  },
  methods: {
    agregarPersona(persona) {
      let id = 0

      if (this.personas.length > 0) {
        id = this.personas[this.personas.length - 1].id + 1
      }

      this.personas = [...this.personas, {...persona, id}]
    },
    eliminarPersona(id) {
      this.personas = this.personas.filter(
          persona => persona.id !== id
      );
    },
    actualizarPersona(id, personaActualizada) {
      this.personas = this.personas.map(persona =>
        persona.id === id ? personaActualizada : persona
      );
    },
  }
}
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }
</style>
