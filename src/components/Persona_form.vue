<template>
  <v-card outlined>
    <v-form 
      lazy-validation
      @submit.prevent="save"
      method="post" 
      id="frmPersona">
      <v-card-title>
        <h3>{{ isNew ? "Nuevo" : "Actualizar" }} Consultor o Supervisor</h3>
        <v-spacer />
        <v-btn icon color="red" @click="salir" outlined>
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </v-card-title>
      <v-divider />
      <v-card-text>
        <v-container style="margin-bottom: -30px; margin-top: -20px">
          <v-row>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="consultor.ci"
                label="Cedula de Identidad *"
                required
                type="text"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="consultor.id"
                label="N.I.T."
                type="text"
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row style="margin-top: -20px">
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.paterno"
                label="Apellido Paterno *"
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.materno"
                label="Apellido Materno"
                required
                type="text"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.nombres"
                label="Nombres *"
                type="text"
                required
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row style="margin-top: -20px">
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.fechaNacimiento"
                label="Fecha Nacimiento *"
                type="Date"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.fono1"
                label="Telefono/Celular 1 *"
                required
                type="text"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.fono2"
                label="Telefono/Celular 2"
                type="text"
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row style="margin-top: -20px">
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.email"
                label="Correo Electronico *"
                type="email"
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.grado"
                label="Grado Academico"
                type="text"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="consultor.genero"
                label="Genero *"
                type="text"
                required
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row style="margin-top: -20px">
            <v-col cols="12" md="12">
              <v-text-field
                v-model="consultor.direccion"
                label="Direccion Domiciliaria *"
                required
                type="text"
              ></v-text-field>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-divider />
      <v-card-actions style="margin-top: 10px">
        <v-spacer />
        <v-btn 
        type="submit" 
        color="green"
        
        outlined
         :loading="loading"
         > GUARDAR </v-btn>
      </v-card-actions>
    </v-form>
    <pre>
      {{ consultor }}
    </pre>
  </v-card>
</template>

<script>
import { mapState } from "vuex";
export default {
  name: "Persona_form",
  props: ["persona"],
  data: () => ({
    isNew: true,
    consultor: {},
    loading:false,
    errores: null,
  }),
  computed: {
    ...mapState(["url"]),
  },
  created() {
    if (this.persona == null) this.isNew = true;
    else this.isNew = false;
  },
  mounted() {
    if (!this.isNew) this.getPersona();
  },
  methods: {
    salir() {
      this.$emit("salir");
    },
     getPersona() {
      const url = this.url + "personas/" + this.persona.id;
      this.axios.get(url).then((response) => {
        this.consultor = response.data;
      });
    },
    save() {
       
      let url ="";
      if(this.isNew)
             url = this.url + "personas/" 
     else
             url = this.url + "personas/" + this.persona.id;
    this.loading = true;
      this.axios({
        method: this.isNew ? 'POST': 'PUT',
        url:url,
        data: this.consultor,
      }).then(response => {
        if (response.data.res === true){
           this.$toastr.success(response.data.message);
          }else
           this.$toastr.error(response.data.message);
      }).catch(e =>{
        console.log(e.response.data.errors);
         this.errores = e.response.data.errors;
      }).finally(()=> {
        this.loading =false;
         this.salir();
      })
    },
  },
};
</script>

<style scoped>
</style>