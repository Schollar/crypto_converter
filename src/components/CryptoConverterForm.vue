<template>
  <div>
    <form class="crypto_form">
      <v-select
        return-object
        :items="crypto_data"
        item-text="name"
        v-on:input="formatPrice()"
        label="Standard"
        v-model="selected"
        class="select"
      ></v-select>
    </form>
    <p>Price USD: {{ selected.priceUsd }}</p>
    <currency-converter-selector
      :currencies="currencies"
      @input="selection_changed"
      v-model="selected_currency"
    ></currency-converter-selector>
    <p>
      Price {{ selected_currency.name }}:
      {{ selected.priceUsd * selected_currency.price }}
    </p>
  </div>
</template>

<script>
import CurrencyConverterSelector from "./CurrencyConverterSelector.vue";
export default {
  name: "crypto-converter",
  components: {
    CurrencyConverterSelector,
  },
  mounted() {
    this.get_crypto_data();
  },
  methods: {
    selection_changed(value) {
      console.log(value);
    },
    formatPrice: function () {
      let num = Number(this.selected["priceUsd"]);
      this.selected["priceUsd"] = num.toFixed(4);
    },
    get_crypto_data() {
      // Grabbing the availible coins and storing them in our data
      this.$axios
        .request({
          url: `https://api.coincap.io/v2/assets`,
          method: "GET",
        })
        // Setting character tasks list to data sent back
        .then((response) => {
          this.crypto_data = response.data.data;
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
  data() {
    return {
      crypto_data: undefined,
      selected: {
        priceUsd: 0,
      },
      currencies: ["CAD", "EUR", "GBP"],
      selected_currency: {
        name: "You must pick a currency first!",
        price: "",
      },
    };
  },
};
</script>

<style scoped>
.crypto_form {
  border: 1px solid black;
}
</style>