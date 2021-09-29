<template>
  <v-card 
   outlined
   :loading="loading"
   >
    <v-card-title>
      SUPERVISORES / CONSULTORES
      <v-spacer />
      <v-btn  
          @click="dialog = !dialog"
      > <span class="mr-2">NUEVO : CONSULTOR/SUPERVISOR</span></v-btn>
    </v-card-title>
    <v-divider />

    <v-card-text>
      <v-row>
        <v-col cols="10" md="10" sm="12">
          <v-text-field
            v-model ="txtBuscar"
            label="Buscar por nombre o C.I."
            outlined
            dense
          ></v-text-field>
        </v-col>
        <v-col cols="2" md="2" sm="12">
          <v-btn color="primary" @click="getPersonas"
          > Buscar </v-btn>
        </v-col>
      </v-row>

      <v-row style="margin-top: -30px">
        <v-col
          cols="12"
          md="12"
          sm="12"
          v-for="(row, index) in consultores"
          :key="index"
        >
          <Persona :consultor ="row" />
        </v-col>
      </v-row>
       <v-dialog v-model="dialog" max-width="850" persistent>
           <NEPersona  @salir="salir"   />
  
       </v-dialog>
    </v-card-text>
    
  </v-card>
  

</template>

<script>
import { mapState } from 'vuex';
import Persona from "../components/Persona";
import NEPersona from "../components/Persona_form";

export default {
  components: { Persona,NEPersona },
  name: "Personas",
  data: () => ({
    consultores: [],
    dialog: false,
    loading: false,
    txtBuscar: ""
  }),
  computed:{
    ...mapState(['url'])
  },
  mounted(){
    this.getPersonas()
  },
  methods: {
      salir() {
      this.dialog = false;
    },
    getPersonas(){
       this.loading =true;
      const url = this.url+"personas"+"?txtBuscar="+this.txtBuscar ;   
      this.axios.get(url).then(response =>{
        // todo lo que trae el backend
        console.log(response.data);
        this.consultores = response.data;
        this.loading = false;
      })
    }

  }
};
</script>
