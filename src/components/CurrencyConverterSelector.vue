<template>
  <div>
    <!-- TO DO: use https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies.json to grab list exchange rate for and make a list of maybe top 10 currencies to convert to -->
    <v-select
      :items="currencies"
      label="Standard"
      v-model="selected"
      class="select"
    ></v-select>
  </div>
</template>

<script>
export default {
  name: "currency-converter-selector",
  data() {
    return {
      currency_data: undefined,
      currencies: ["CAD", "EUR", "GPB"],
    };
  },
  mounted() {
    this.get_currency_data();
  },
  methods: {
    get_currency_data() {
      // Grabbing The prices of other currencies using USD as the base
      this.$axios
        .request({
          url: `https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies/usd.json`,
          method: "GET",
        })
        // Setting character tasks list to data sent back
        .then((response) => {
          response.forEach();
          this.currency_data = response.data.usd;
        })
        .catch((error) => {
          error;
          this.$root.$emit(
            "error_message",
            "Something went wrong getting characters tasks"
          );
        });
    },
  },
};
</script>

<style scoped>
</style>