<template>
  <v-app>
    <v-main> <crypto-converter /> </v-main>
  </v-app>
</template>

<script>
import CryptoConverter from "./components/CryptoConverterForm.vue";
export default {
  name: "App",

  components: { CryptoConverter },

  data: () => ({
    //
  }),
};
</script>
