<template>
  <v-card elevation="2" outlined>
    <v-toolbar color="pink" dark dense flat>
      <v-toolbar-title class="text-body-3">
        <v-icon>mdi-card-account-details</v-icon>
        {{ consultor.ci }} | {{ consultor.datosp }}
      </v-toolbar-title>
    </v-toolbar>
    <v-card-text>
      <v-list class="transparent" style="margin-bottom: -20px">
        <v-list-item style="margin-bottom: -20px">
          <v-list-item-icon>
            <v-icon>mdi-school</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left"
            >GRADO ACADÉMICO:
          </v-list-item-title>
          <v-list-item-subtitle class="text-left">
            {{ consultor.grado }}
          </v-list-item-subtitle>
        </v-list-item>

        <v-list-item style="margin-bottom: -20px">
          <v-list-item-icon>
            <v-icon>mdi-calendar-range</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left"
            >FECHA DE NACIMIENTO:
          </v-list-item-title>
          <v-spacer />
          <v-list-item-subtitle class="text-left">
            {{ consultor.fechaNacimiento }}
          </v-list-item-subtitle>
        </v-list-item>

        <v-list-item style="margin-bottom: -20px">
          <v-list-item-icon>
            <v-icon>mdi-phone</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left"
            >TELEFONO/CELULAR 1:
          </v-list-item-title>
          <v-spacer />
          <v-list-item-subtitle class="text-left">
            {{ consultor.fono1 }}
          </v-list-item-subtitle>
        </v-list-item>

        <v-list-item style="margin-bottom: -20px">
          <v-list-item-icon>
            <v-icon>mdi-phone</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left"
            >TELEFONO/CELULAR 2:
          </v-list-item-title>
          <v-spacer />
          <v-list-item-subtitle class="text-left">
            {{ consultor.fono2 }}
          </v-list-item-subtitle>
        </v-list-item>

        <v-list-item style="margin-bottom: -20px">
          <v-list-item-icon>
            <v-icon>mdi-email</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left"
            >CORREO ELECTRÓNICO:
          </v-list-item-title>
          <v-spacer />
          <v-list-item-subtitle class="text-left">
            {{ consultor.email }}
          </v-list-item-subtitle>
        </v-list-item>

        <v-list-item style="margin-bottom: -20px">
          <v-list-item-icon>
            <v-icon>mdi-map-marker</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left">DIRECCION: </v-list-item-title>
          <v-spacer />
          <v-list-item-subtitle class="text-left">
            {{ consultor.direccion }}
          </v-list-item-subtitle>
        </v-list-item>

        <v-list-item style="margin-bottom: -20px">
          <v-list-item-icon>
            <v-icon>mdi-card-account-details</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left">N.I.T. : </v-list-item-title>
          <v-spacer />
          <v-list-item-subtitle class="text-left">
            {{ consultor.nit }}
          </v-list-item-subtitle>
        </v-list-item>
        <v-list-item>
          <v-list-item-icon>
            <v-icon>mdi-gender-male-female</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left">GENERO : </v-list-item-title>
          <v-spacer />
          <v-list-item-subtitle class="text-left">
            {{ consultor.genero }}
          </v-list-item-subtitle>
        </v-list-item>
      </v-list>
    </v-card-text>

    <v-divider />
    <v-card-subtitle>
      <v-row style="margin-top: -12px">
        <v-spacer />
        <v-btn color="green" depressed @click="dialog = !dialog">
          <span class="mr-0"> Editar registro</span>
        </v-btn>
      </v-row>
    </v-card-subtitle>

    <v-dialog v-model="dialog" max-width="850" persistent>
      <NEPersona
        :persona="consultor"
        @salir="salir"
        @listar="$emit('actualizar')"
      />
    </v-dialog>
  </v-card>
</template>

<script>
import NEPersona from "../components/Persona_form";
export default {
  name: "Persona",
  components: { NEPersona },
  props: ["consultor"],
  data: () => ({
    dialog: false,
    forecast: [
      {
        day: "Grado. Academico :",
        icon: "mdi-school",
        temp: "consultor.grado",
      },
      {
        day: "Fecha Nac.:",
        icon: "mdi-calendar-range",
        temp: "fechaNacimiento",
      },
      { day: "Telefono/Celular 1 :", icon: "mdi-phone", temp: "fono1" },
      { day: "Telefono/Celular 2 :", icon: "mdi-phone", temp: "fono2" },
      { day: "Email :", icon: "mdi-email", temp: "email" },
      { day: "Direccion :", icon: "mdi-map-marker", temp: "direccion" },
      { day: "Nit :", icon: "mdi-card-account-details", temp: "nit" },
      { day: "Genero :", icon: "mdi-gender-male-female", temp: "genero" },
    ],
  }),

  methods: {
    salir() {
      this.dialog = false;
    },
  },
};
</script>

<style scoped>
</style>