<template>
  <v-card
      elevation="2"
      outlined
  >
    <v-card-title>
      <h4>
       {{consultor.ci}} | {{consultor.nombres}} |  {{consultor.genero}}
      </h4>
      <v-spacer>

      </v-spacer> 
         <v-btn
          color="green"
          text
           outlined
           
          @click="dialog = !dialog"> <span class="mr-2">
          Editar</span>
        </v-btn>


     </v-card-title>

    <v-divider/>
    <div >
      <v-chip  class="ma-2"
               color="primary">  {{consultor.grado}}
         </v-chip>
      <v-chip  class="ma-2"
               color="primary">  {{consultor.nit}}
         </v-chip>

      <v-chip class="ma-2"
              color="secondary"> {{consultor.fechaNacimiento}} </v-chip>

      <v-chip class="ma-2"
              color="red"
              text-color="white">{{consultor.fono1}}</v-chip>

      <v-chip class="ma-2"
              color="green"
              text-color="white">{{consultor.fono2}}</v-chip>
      <v-chip class="ma-2"
              color="orange"
              text-color="white">{{consultor.email}}</v-chip>
      <v-chip class="ma-2"
              color="red"
              text-color="white">{{consultor.direccion}}</v-chip>
              <v-chip class="ma-2"
              color="red"
              text-color="white">{{consultor.observacion}}</v-chip>

<v-dialog v-model="dialog" max-width="850" persistent>
           <NEPersona :persona="consultor" @salir="salir"   />
       </v-dialog>
    </div>

  </v-card>

</template>

<script>
import NEPersona from "../components/Persona_form";
export default {
  name: "Persona",
  components:{NEPersona},
  props:['consultor'],
   data: () => ({
     dialog: false,
   }),

  methods:{
     openForm(){
      this.$router.push({name: 'NEPersona'})
    },
    salir() {
      this.dialog = false;
    },
  },


}
</script>

<style scoped>

</style>