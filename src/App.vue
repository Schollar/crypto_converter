<template>
  <v-app>
    <v-main>
      <page-header></page-header>
      <crypto-converter />
      <page-footer />
    </v-main>
  </v-app>
</template>

<script>
import CryptoConverter from "./components/CryptoConverterForm.vue";
import PageHeader from "./components/PageHeader.vue";
import PageFooter from "./components/PageFooter.vue";
export default {
  name: "App",

  components: { CryptoConverter, PageHeader, PageFooter },

  data: () => ({
    //
  }),
};
</script>

<style scoped>
.v-main {
  display: grid;
  justify-items: center;
  text-align: center;
  position: relative;
  background-color: #454955;
}
</style>
