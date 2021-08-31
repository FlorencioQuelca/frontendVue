<template>
  <v-card
  outlined
  >
    <v-card-title>
      <h3>Inicio de Sesion / Register </h3>
      <v-spacer>

      </v-spacer>
      <v-btn
        outlined
      text
      @click="salir"
      >
        salir
      </v-btn>
    </v-card-title>
      <v-divider/>

    <v-radio-group
        style="margin-left: 100px">
      <v-radio
          value="uno"
          label="Persona Natural o Consulor"
      ></v-radio>
      <v-radio
          value="dos"
          label="Empresa Publica o Privada"
      ></v-radio>
      <v-radio
          value="tres"
          label="Asociación o Sociedad Accidental"
      ></v-radio>
    </v-radio-group>

    <v-divider/>
    <v-card-text>
    <v-form
      lazy-validation>
      <v-text-field
      label="Email *"
      type="email"
      required
      v-model="email"
      >
      </v-text-field>
      <v-text-field
          label="Password *"
          type="password"
          required
          v-model="password"
      >
      </v-text-field>
    </v-form>
    </v-card-text>
    <v-card-actions style="margin-top: -30px">
      <v-btn
           color="green"
            block
           type="submit">
        Aceptar
      </v-btn>
    </v-card-actions>
    <v-card-actions>
      <v-btn
          color="red"
          block
      >
        Registrarse
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "Login",
  data: () => ({
    email: "",
    password: "",
  }),
  methods: {
    salir() {
      this.$emit("salir")
    },


  }
}
</script>

<style scoped>

</style>