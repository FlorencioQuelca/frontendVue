<template>
  <v-card
      elevation="2"
      outlined
  >
    <v-card-title>
      <h4>
        {{proyecto.codigo}}
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
               color="primary">   {{proyecto.nombre}}
         </v-chip>

      <v-chip class="ma-2"
              color="secondary"> {{proyecto.fecha}} </v-chip>

      <v-chip class="ma-2"
              color="red"
              text-color="white">{{proyecto.hora}}</v-chip>

      <v-chip class="ma-2"
              color="green"
              text-color="white">{{proyecto.precio}}</v-chip>
      <v-chip class="ma-2"
              color="orange"
              text-color="white">{{proyecto.plazoEntrega}}</v-chip>
      <v-chip class="ma-2"
              color="red"
              text-color="white">{{proyecto.link}}</v-chip>


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