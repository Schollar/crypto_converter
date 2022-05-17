<template>
  <v-app>
    <v-main>
      <page-header></page-header>
      <crypto-converter />
    </v-main>
  </v-app>
</template>

<script>
import CryptoConverter from "./components/CryptoConverterForm.vue";
import PageHeader from "./components/PageHeader.vue";
export default {
  name: "App",

  components: { CryptoConverter, PageHeader },

  data: () => ({
    //
  }),
};
</script>

<style scoped>
.v-main {
  display: grid;
  justify-items: center;
  position: relative;
  background-color: darkgray;
}
</style>
