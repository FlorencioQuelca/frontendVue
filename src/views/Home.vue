<template>
   <div >
     <v-row
         align="center"
         justify="center"
     >
       <v-img
           :src="require('../assets/agua.png')"
           max-width="800"
           max-height="800"
       >
       </v-img>
       </v-row>
     <v-row align="center"
     justify="center">
     <v-btn>
         welcome
       </v-btn>
     </v-row>

   </div>


</template>



<script>


  export default {
    name: 'Home',
    components: {

    },
  }
</script>
