<template>
  <v-card
      outlined>
    <v-card-title >
      proyectos vigentes

    </v-card-title>
    <v-divider/>

    <v-card-text>
      <v-row>
        <v-col> </v-col>
      </v-row>

      <v-row >
        <v-col cols="12" md="12" sm="12" v-for="(row,index) in proyectos" :key="index" >
         <Proyecto></Proyecto>

        </v-col>

      </v-row>



    </v-card-text>
  </v-card>
</template>

<script>
import Proyecto from "../components/Proyecto";
export default {
  name: "Personas",
  components: {Proyecto},
  data:() =>({
    proyectos:[
      {id:1},
      {id:2},
      {id:3},
      {id:4},
      {id:5},
      {id:6},
    ]
  })
}
</script>

<style scoped>

</style>