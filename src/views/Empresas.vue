<template>
  <v-card 
   outlined
   :loading="loading"
   >
    <v-card-title>
      EMPRESAS       <v-spacer />
      <v-btn  
          @click="dialog = !dialog"
      > <span class="mr-2">NUEVA : EMPRESA</span></v-btn>
    </v-card-title>
    <v-divider />
    <v-card-text>
      <v-row>
        <v-col cols="10" md="10" sm="12">
          <v-text-field
            v-model ="txtBuscar"
            label="Buscar por nombre N.I.T."
            outlined
            dense
            @change="getEmpresas"
          ></v-text-field>
        </v-col>
        <v-col cols="2" md="2" sm="12">
          <v-btn color="primary" @click="getEmpresas"
          > Buscar </v-btn>
        </v-col>
      </v-row>
      
     
      <v-row style="margin-top: -30px">
        <v-col
          cols="12"
          md="6"
          sm="6"
          v-for="(row, index) in empresas"
          :key="index"
        >
          <Empresa :empre ="row"
            @actualizar="getEmpresas" 
         />
        </v-col>
      </v-row>
      <v-dialog v-model="dialog" max-width="850" persistent>
           <NEEmpresa  @salir="salir"  @listar="getEmpresas" />
       </v-dialog>
       
    </v-card-text>
    
  </v-card>
  

</template>

<script>
import { mapState } from 'vuex';
import Empresa from "../components/Empresa";
import NEEmpresa from "../components/Empresa_form";

export default {
  components: { Empresa,NEEmpresa },
  name: "Empresas",

  data: () => ({
    select: { state: "MASCULINO", abbr: "M" },
    genero: [
      { state: "MASCULINO",abbr: "M" },
      { state: "FEMENINO" ,abbr: "F"},
    ],
    empresas: [],
    dialog: false,
    loading: false,
    txtBuscar: ""
  }),
  computed:{
    ...mapState(['url'])
  },
  mounted(){
    this.getEmpresas()
  },
  methods: {
      salir() {
      this.dialog = false;
    },
    getEmpresas(){
      
       this.loading =true;
      const url = this.url+"empresas"+"?txtBuscar="+this.txtBuscar ;   
      this.axios.get(url).then(response =>{
        // todo lo que trae el backend
        if (response.data.length ===0)
        {
          this.$toastr.error("no encontrado");
          this.loading = false;
           this.empresas = response.data;
        }else 
        {
        console.log(response.data);
          if (response.data.length ===1 && this.txtBuscar!="")
                          this.$toastr.success("encontrado");
        this.empresas = response.data;
        this.loading = false;
        }
      })
    }

  }
};
</script>
