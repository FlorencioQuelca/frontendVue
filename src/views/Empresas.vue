<template>
  <v-card
   outlined
   :loading="loading">
  <v-card-title >
      <h3>
        PROYECTOS VIGENTES PARA:
      </h3>
      <v-spacer/>
    <v-radio-group
        style="margin-left: 100px"
        row>
      <v-radio
          value="uno"
          label="Vigentes"
      ></v-radio>
      <v-radio
          value="dos"
          label="Todos"
      ></v-radio>
    </v-radio-group>
    <v-select
        v-model="select"
        :hint="`${select.state}, ${select.abbr}`"
        :items="items"
        item-text="state"
        item-value="abbr"
        label="Select"
        persistent-hint
        return-object
        single-line
    ></v-select>

   <v-btn
      outlined
      color="green">
       BUSCAR
   </v-btn>
  </v-card-title>
    <v-divider/>

    <v-card-text>
      <v-row>
         <v-col> </v-col>
      </v-row>
      <v-row style="margin-top: -40px">
        <v-col cols="12" md="12" sm="12" v-for="(row,index) in proyectosl" :key="index" >
          <Proyecto :proyecto="row"></Proyecto>
        </v-col>
      </v-row>

    </v-card-text>
    </v-card>

</template>

<script>
import Proyecto from "../components/Proyecto";
import {mapState} from "vuex";

export default {
  name: "Empresas",
  components: {Proyecto},
  data:() =>({
    select: { state: 'LA PAZ', abbr: 'Lp' },
    items: [
      { state: 'LA PAZ', abbr: 'Lp' },
      { state: 'Cochabamba', abbr: 'Cbba' },
      { state: 'Santa Cruz', abbr: 'Sc' },
      { state: 'Potosi', abbr: 'Pt' },
      { state: 'Oruro', abbr: 'Or' },
      { state: 'Tarija', abbr: 'Tr' },
      { state: 'Pando', abbr: 'Pd' },
      { state: 'Beni', abbr: 'Bn' },
      { state: 'Chuquisaca', abbr: 'Ch' },
    ],

    proyectosl:[],
    loading:false,

  }),
  computed:{
    ...mapState(['url'])
  },
  mounted() {
  this.getEmpresas();
    },
  methods:{
    getEmpresas: function () {
      this.loading = true;
      var hoy = new Date();
      const url = this.url + 'proyectoEmpresa/';
      this.axios.get(url, { params: {
          hora: hoy.getHours()+':'+hoy.getMinutes()+':'+hoy.getSeconds(),
          fecha: hoy.getFullYear()+'-'+(hoy.getMonth()+1)+'-'+hoy.getDay(),
          departamento: this.select.state,
        }
        }).then(response => {
        //todo lo que trae del backend
        console.log(response.data);
        this.proyectosl = response.data;
        this.loading = false;
      })
    }
  },
}
</script>

<style scoped>

</style>