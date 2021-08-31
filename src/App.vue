<template>
  <v-app>
    <v-app-bar
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          class="shrink mr-2"
          contain
          :src="require('./assets/fps.png')"
          transition="scale-transition"
          width="40"

        />
        <v-btn
            contain
            text
            @click="openHome"
        >
          <h2> FPS - LA PAZ</h2>
        </v-btn>

      </div>

      <v-spacer/>
      <v-item-group>

      <v-btn

          text
          @click="openPersonas"
      >
        <span class="mr-2">CONVOCATORIAS para CONSULTORES</span>
      </v-btn>
      <v-btn
             text
          @click="openEmpresas"
      >
        <span class="mr-2">CONVOCATORIAS para EMPRESAS</span>
      </v-btn>

      <v-btn
         text
        @click="dialog = !dialog"
      >
        <span class="mr-2">Login</span>
      </v-btn>
      <v-btn
          text
      >
        SALIR
        <v-avatar color="indigo">
          <v-icon dark>
            mdi-account-circle
          </v-icon>
        </v-avatar>
      </v-btn>
      </v-item-group>

    </v-app-bar>

    <v-main
    class ="grey lighten-2"
    >
      <v-container >
            <router-view/>
      </v-container>

    </v-main>
    <v-dialog
        v-model="dialog"
        max-width="450"
        persistent
    >
      <login
      @salir="salir"/>
    </v-dialog>
    <Footer></Footer>

  </v-app>
</template>

<script>


import Footer from "./components/Footer";
import Login from "./components/Login";
export default {
  name: 'App',

  components: {Login, Footer},

  data: () => ({
    items: [
      { title: 'para Personas Naturales y/o Consultores' },
      { title: 'para Empresas y Asociaciones ' },
        ],
    dialog:false,
  }),
  methods: {
      openEmpresas(){
      this.$router.push({name:'Empresas'})
      },
     openHome(){
      this.$router.push({name:'Home'})
    },
    openPersonas(){
      this.$router.push({name: 'Personas'})
    },
    salir(){
        this.dialog = false
    }


  },



};
</script>
