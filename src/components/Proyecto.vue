<template>
  <v-card
      elevation="2"
      outlined
  >
    <v-card-title>
      <h4>
        {{proyecto.id}}
      </h4>
      <v-spacer>

      </v-spacer>
         <v-btn
          color="green"
          text
        outlined
        >
          Presentarse
        </v-btn>


     </v-card-title>

    <v-divider/>
    <div >
      <v-chip  class="ma-2"
               color="primary"> nombre completo
         </v-chip>

      <v-chip class="ma-2"
              color="secondary"> fecha </v-chip>

      <v-chip class="ma-2"
              color="red"
              text-color="white">hora</v-chip>

      <v-chip class="ma-2"
              color="green"
              text-color="white">costo ref.</v-chip>
      <v-chip class="ma-2" >dias.</v-chip>
      <v-chip class="ma-2"
              color="red"
              text-color="white">link</v-chip>


    </div>

  </v-card>

</template>

<script>
export default {
  name: "Proyecto",

  props:['proyecto'],

}
</script>

<style scoped>

</style>