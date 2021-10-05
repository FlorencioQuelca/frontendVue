<template>
  <v-card 
   outlined
   :loading="loading"
   >
    <v-card-title>
      SOCIEDADES ACCIDENTALES      <v-spacer />
      <v-btn  
          @click="dialog = !dialog"
      > <span class="mr-2">NUEVA : SOCIEDAD</span></v-btn>
    </v-card-title>
    <v-divider />
    <v-card-text>
      <v-row>
        <v-col cols="10" md="10" sm="12">
          <v-text-field
            v-model ="txtBuscar"
            label="Buscar por NOMBRE o CODIGO REGISTRO "
            outlined
            dense
            @change="getSociedades"
          ></v-text-field>
        </v-col>
        <v-col cols="2" md="2" sm="12">
          <v-btn color="primary" @click="getSociedades"
          > Buscar </v-btn>
        </v-col>
      </v-row>
      
     
      <v-row style="margin-top: -30px">
        <v-col
          cols="12"
          md="6"
          sm="6"
          v-for="(row, index) in sociedades"
          :key="index"
        >
          <Sociedad :empre ="row"
            @actualizar="getSociedades" 
         />
        </v-col>
      </v-row>
      <v-dialog v-model="dialog" max-width="850" persistent>
           <NESociedad  @salir="salir"  @listar="getSociedades" />
       </v-dialog>
       
    </v-card-text>
    
  </v-card>
  

</template>

<script>
import { mapState } from 'vuex';
import Sociedad from "../components/Sociedad";
import NESociedad from "../components/Sociedad_form";

export default {
  components: { Sociedad,NESociedad },
  name: "Sociedades",

  data: () => ({
    select: { state: "MASCULINO", abbr: "M" },
    genero: [
      { state: "MASCULINO",abbr: "M" },
      { state: "FEMENINO" ,abbr: "F"},
    ],
    sociedades: [],
    dialog: false,
    loading: false,
    txtBuscar: ""
  }),
  computed:{
    ...mapState(['url'])
  },
  mounted(){
    this.getSociedades()
  },
  methods: {
      salir() {
      this.dialog = false;
    },
    getSociedades(){

       this.loading =true;
      const url = this.url+"sociedadAccidentals"+"?txtBuscar="+this.txtBuscar ;   
      this.axios.get(url).then(response =>{
        // todo lo que trae el backend
        if (response.data.length ===0)
        {
          this.$toastr.error("no encontrado");
          this.loading = false;
           this.sociedades = response.data;
        }else 
        {
        console.log(response.data);
          if (response.data.length ===1 && this.txtBuscar!="")
                          this.$toastr.success("encontrado");
        this.sociedades = response.data;
        this.loading = false;
        }
      })
    }

  }
};
</script>
