<template>
  <div>
    <!-- TO DO: use https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies.json to grab list exchange rate for and make a list of maybe top 10 currencies to convert to -->
    <v-select
      return-object
      :items="crypto_data"
      item-text="name"
      label="Standard"
      v-model="selected"
      class="select"
    ></v-select>
  </div>
</template>

<script>
export default {
  name: "currency-converter-selector",
};
</script>

<style scoped>
</style>