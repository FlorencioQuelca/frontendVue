
<template>
  <v-footer
      dark
      padless
  >
    <v-card
        class="flex"
        flat
        tile
    >
      <v-card-title class="teal">
        <strong class="subheading">Estamos Saliendo Adelante , Fondo Nacional de Inversion Productiva y Social</strong>

        <v-spacer></v-spacer>

        <v-btn
            v-for="icon in icons"
            :key="icon"
            class="mx-4"
            dark
            icon
            href="https://www.facebook.com/fpslapaz"

        >
          <v-icon size="24px">
            {{ icon }}
          </v-icon>
        </v-btn>

      </v-card-title>

      <v-card-text class="py-2 white--text text-center">
        {{ new Date().getFullYear() }} — <strong>FPS - LA PAZ</strong>
      </v-card-text>
    </v-card>
  </v-footer>
</template>

<script>
export default {
  name: "Footer",
  data: () => ({
    icons: [
      'mdi-facebook',
    ],
  }),
}
</script>

<style scoped>

</style>