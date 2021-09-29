<template>
  <v-card outlined>
    <v-card-title> SOCIEDADES ACCIDENTALES </v-card-title>
    <v-divider />

    <v-card-text>
      <v-row>
        <v-col> </v-col>
      </v-row>

      <v-row>
        <v-col
          cols="12"
          md="12"
          sm="12"
          v-for="(row, index) in persons"
          :key="index"
        >
          <ListaPersonas />
        </v-col>
      </v-row>
    </v-card-text>
  </v-card>
</template>

<script>
import ListaPersonas from "../components/Persona";
export default {
  components: { ListaPersonas },
  name: "Sociedades",
  // components: {Proyecto},
  data: () => ({
    persons: [{ id: 1 }, { id: 2 }, { id: 3 }, { id: 4 }, { id: 5 }, { id: 6 }],
  }),
};
</script>

<style scoped>
</style>