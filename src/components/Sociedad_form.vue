<template>
  <v-card outlined>
    <v-form
      ref="form"
      lazy-validation
       v-model="valid"
      @submit.prevent="save"
      
    >
    <v-toolbar color="pink" dark dense flat>
      
      <v-toolbar-title class="text-body-3">
          <h3>{{ isNew ? "Registrar nueva" : "Actualizar datos de " }} ASOCIACION ACCIDENTAL </h3>
      </v-toolbar-title>
       <v-spacer/>
          <v-btn  color="white" @click="salir" outlined>
            <v-icon>mdi-close</v-icon>          
        </v-btn>
    </v-toolbar>


      <v-card-text>
        <errores
         v-if="errores !== null" 
          :errores="errores"
        ></errores>
        <v-container style="margin-bottom: -30px; margin-top: -20px">
          <v-row>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="empresa1.nit"
                label="codigo Interno * (Ejemplo: 220210001)"
                required
                type="number"
                :rules="[
                    (v) => !!v || 'nit requerido',
                    v => (v && v.length >= 1  && v.length <=11) || 'Cantidad de Caracteres invalido',
                ]"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="8">
              <v-text-field
                v-model="empresa1.nombre"
                label="Nombre de la asociacion accidental "
                type="text"
                :rules="[
                    (v) => !!v || 'nombre requerido',
                ]"
                 
              ></v-text-field>
            </v-col>
          </v-row>

          <v-row style="margin-top: -20px">
              <v-spacer/>
            <v-col cols="12" md="8">
              <v-text-field
                v-model="empresa1.nombreLegal"
                label="Nombre completo Representante Legal *"
         
                :rules="[
                    (v) => !!v || 'Nombre completo representante legal Requerido',
                    v => (v && v.length >= 3  && v.length <=100) || 'Cantidad de caracteres invalido',
                ]"
              ></v-text-field>
            </v-col>
         
          </v-row>
          <v-row style="margin-top: -20px">
           
            <v-col cols="12" md="4">
              <v-text-field
                v-model="empresa1.fono1"
                label="Telefono o Celular 1 *" 
                type="number"
                required
                :rules="[
                    (v) => !!v || 'Numero de celular o telefono requerido',      
                ]"
               
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="empresa1.fono2"
                label="Telefono/Celular 2"
                type="number"
              ></v-text-field>
            </v-col>
             <v-col cols="12" md="4">
              <v-text-field
                v-model="empresa1.email"
                label="Correo Electronico *"
                type="email"
      
                :rules="[
                    v => !!v || 'Correo electronio requerido',
                    v => (v && v.length >= 7  && v.length <=50) || 'Cantidad de caracteres invalido',
                    v => (v || '').indexOf(' ') < 0 ||  'no se permite spacios en blanco',
                    v => /.+@.+\..+/.test(v) || 'correo invalido',
                ]"
              ></v-text-field>
            </v-col>
          </v-row>

          <v-row style="margin-top: -20px">
            
            <v-col cols="12" md="4">
              <v-select
                v-model="empresa1.departamento"
                label="Departamento"
                type="text"
                :items="items1"
                :rules="[v => !!v || 'Departamento es requerido']"
              ></v-select>
            </v-col>
            
      
            <v-col cols="12" md="8">
              <v-text-field
                v-model="empresa1.observacion"
                label="Direccion Domiciliaria *"


                :rules="[
                    v => !!v || 'direccion domiciliaria requerido',
                  
                ]"
              ></v-text-field>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-divider />
      <v-card-actions style="margin-top: 10px">
       
        <v-spacer />
        <v-btn 
         :disabled="!valid"
        type="submit"
        color="success"
        :loading="loading">
          GUARDAR
        </v-btn>
      </v-card-actions>
    </v-form>
        
  </v-card>
</template>

<script>
import { mapState } from "vuex";
import errores from './errores.vue';
export default {
  components: { errores },
  name: "Sociedad_form",
  props: ["empresa"],
  data: () => ({
    isNew: true,
    empresa1: {  
                 },
    loading: false,
    valid:true,
    errores: null,
     
     items1: [
        'LA PAZ',
        'ORURO.',
        'POTOSI',
        'COCHABAMBA',
        'SANTA CRUZ',
        'TARIJA',
        'PANDO',
        'BENI',
        'CHUQUISACA',
      ],
  }),
  computed: {
    ...mapState(["url"]),
  },
  created() {
    if (this.empresa == null) 
        this.isNew = true;
    else this.isNew = false;
  },
  mounted() {
    if (!this.isNew) this.getEmpresa();
  },
  methods: {
    salir() {
      this.$emit("salir");
    },
     listar() {
      this.$emit("listar");
    },
    getEmpresa() {

      const url = this.url + "sociedadAccidentals/" + this.empresa.id;
      this.axios.get(url).then((response) => {
       
        // console.log(response.data);
         this.empresa1 = response.data;
                    
      });
    },
    save() {
      if (!this.$refs.form.validate())
             return;
      let url = "";
      this.errores =null;
     this.empresa1.nombreLegal= this.empresa1.nombreLegal.toUpperCase();
     this.empresa1.nombre= this.empresa1.nombre.toUpperCase();
     this.empresa1.direccion= this.empresa1.direccion.toUpperCase();
     this.empresa1.email= this.empresa1.email.toLowerCase();
     
      if (this.isNew) url = this.url + "sociedadAccidentals/";
      else url = this.url + "sociedadAccidentals/" + this.empresa.id;
      this.loading = true;
      this.axios({
        method: this.isNew ? "POST" : "PUT",
        url: url,
        data: this.empresa1,
      })
        .then((response) => {
          if (response.data.res === true ) {
            this.$toastr.success(response.data.message);
             this.listar();
             this.salir();
             
          } else {
            this.errores = response.data.errors;
            this.$toastr.error(response.data.message);
          }
        })
        .catch((e) => {
          //console.log(e.response.data.errors);
          this.errores = e.response.data.errors;
        })
        .finally(() => {
          this.loading = false;  
                 
        });
    },
  },
};
</script>

<style scoped>
</style>