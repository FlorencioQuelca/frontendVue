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
          <h3>{{ isNew ? "Crear nuevo" : "Actualizar datos" }} consultor o supervisor</h3>
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
            <v-col cols="12" md="6">
              <v-text-field
                v-model="consultor.ci"
                label="Cedula de Identidad * (Ejemplo: 5775077-1D)"
                required
                type="text"
                :rules="[
                    (v) => !!v || 'Cedula de Indentidad requerida',
                    v => (v && v.length >= 1  && v.length <=11) || 'Cantidad de Caracteres invalido',
                ]"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="consultor.nit"
                label="N.I.T. (Ejemplo: 5775077013)"
                type="number"
                :rules="[
                    (v) => !!v || 'nit de Indentidad requerida',
                ]"
                 
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row style="margin-top: -20px">
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.paterno"
                label="Apellido Paterno *"
                required
                :rules="[
                    (v) => !!v || 'Apellido Paterno Requerido',
                    v => (v && v.length >= 3  && v.length <=25) || 'Cantidad de caracteres invalido',
                    v => (v || '').indexOf(' ') < 0 ||  'no se permite spacios en blanco'
                ]"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.materno"
                label="Apellido Materno"
                type="text"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.nombres"
                label="Nombres *"
                type="text"
              
                :rules="[
                    (v) => !!v || 'Nombre requerido',
                    v => (v && v.length >= 2  && v.length <=35) || 'Cantidad de caracteres invalido',
                   ]"
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row style="margin-top: -20px">
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.fechaNacimiento"
                label="Fecha Nacimiento *"
                type="Date"
                outlined
                shaped
                :rules="[
                    (v) => !!v || 'fecha de Nacimiento requerido',      
                ]"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.fono1"
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
                v-model="consultor.fono2"
                label="Telefono/Celular 2"
                type="number"
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row style="margin-top: -20px">
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.email"
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
            <v-col cols="12" md="4">
              <v-select
                v-model="consultor.grado"
                label="Grado Academico"
                type="text"
                :items="items1"
                :rules="[v => !!v || 'Grado academico es requerido']"
              ></v-select>
            </v-col>
            <v-col cols="12" md="4">
              <v-select
                v-model="consultor.genero"
                label="Genero *"
                type="text"
                required
                :items="items"
                :rules="[v => !!v || 'Genero is requiredo']"
              ></v-select>
            </v-col>
          </v-row>
          <v-row style="margin-top: -20px">
            <v-col cols="12" md="12">
              <v-text-field
                v-model="consultor.direccion"
                label="Direccion Domiciliaria *"
                type="text"
                :rules="[
                    v => !!v || 'direccion domiciliaria requerido',
                    v => (v && v.length >= 5  && v.length <=300) || 'Cantidad de caracteres invalido',
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
  name: "Persona_form",
  props: ["persona"],
  data: () => ({
    isNew: true,
    consultor: {  genero: null,
                  nombres:null,
                  paterno:null,
                  materno:null,
                  datosp: null,
                  fechaNacimiento:"1900-01-01",
                  grado:'Lic.',
                  fono1:null,
                  
                 },
    loading: false,
    valid:true,
    errores: null,
     
      items: [
        'masculino',
        'femenino',
      ],
      items1: [
        'Lic.',
        'Ing.',
        'Abg.',
        'Dipl.',
        'Phd.',
        'Med.',
        'MSc.',
      ],
  }),
  computed: {
    ...mapState(["url"]),
  },
  created() {
    if (this.persona == null) 
        this.isNew = true;
    else this.isNew = false;
  },
  mounted() {
    if (!this.isNew) this.getPersona();
  },
  methods: {
    salir() {
      this.$emit("salir");
    },
     listar() {
      this.$emit("listar");
    },
    getPersona() {

      const url = this.url + "personas/" + this.persona.id;
      this.axios.get(url).then((response) => {
       
        // console.log(response.data);
         this.consultor = response.data;
                    
      });
    },
    save() {
      if (!this.$refs.form.validate())
             return;
       
         
     this.consultor.datosp = this.consultor.nombres+" "+this.consultor.paterno+" "+ this.consultor.materno;
      let url = "";
      this.errores =null;
      if (this.isNew) url = this.url + "personas/";
      else url = this.url + "personas/" + this.persona.id;
      this.loading = true;
      this.axios({
        method: this.isNew ? "POST" : "PUT",
        url: url,
        data: this.consultor,
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