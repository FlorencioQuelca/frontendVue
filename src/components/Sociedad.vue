<template>
  <v-card elevation="2" outlined>
    <v-toolbar color="pink" dark dense flat>
      <v-toolbar-title class="text-body-3">
        <v-icon>mdi-card-account-details</v-icon>
         {{ empre.nombre}}
      </v-toolbar-title>
    </v-toolbar>
    <v-card-text>
      <v-list class="transparent" style="margin-bottom: -20px">
        <v-list-item style="margin-bottom: -20px">
          <v-list-item-icon>
            <v-icon>mdi-card-account-details</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left"
            >CODIGO ASIGNADO :
          </v-list-item-title>
          <v-list-item-subtitle class="text-left">
            {{ empre.id }}
          </v-list-item-subtitle>
        </v-list-item>

        <v-list-item style="margin-bottom: -20px">
          <v-list-item-icon>
            <v-icon>mdi-account</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left"
            >REPRESENTANTE LEGAL :
          </v-list-item-title>
          <v-spacer />
          <v-list-item-subtitle class="text-left">
            {{ empre.nombreLegal }}
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
            {{ empre.fono1 }}
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
            {{ empre.fono2 }}
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
            {{ empre.email }}
          </v-list-item-subtitle>
        </v-list-item>
  <v-list-item style="margin-bottom: -20px"> 
          <v-list-item-icon>
            <v-icon>mdi-city</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left"> CIUDAD: </v-list-item-title>
          <v-spacer />
          <v-list-item-subtitle class="text-left">
            {{ empre.observacion }}
          </v-list-item-subtitle>
        </v-list-item>

        <v-list-item style="margin-bottom: -20px">
          <v-list-item-icon>
            <v-icon>mdi-map-marker</v-icon>
          </v-list-item-icon>
          <v-list-item-title class="text-left">DIRECCION: </v-list-item-title>
          <v-spacer />
          <v-list-item-subtitle class="text-left">
            {{ empre.direccion }}
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
      <NESociedad
        :empresa="empre"
        @salir="salir"
        @listar="$emit('actualizar')"
      />
    </v-dialog>
  </v-card>
</template>

<script>
import NESociedad from "../components/Sociedad_form";
export default {
  name: "Sociedad",
  components: { NESociedad },
  props: ["empre"],
  data: () => ({
    dialog: false,
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