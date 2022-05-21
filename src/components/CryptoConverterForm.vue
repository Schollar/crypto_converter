<template>
  <div>
    <form class="crypto_form">
      <v-select
        return-object
        :items="crypto_data"
        item-text="name"
        v-on:input="formatUsdPrice()"
        label="Standard"
        v-model="selected"
        class="select"
      ></v-select>
    </form>
    <p>Price USD: ${{ selected.priceUsd }}</p>
    <currency-converter-selector
      :currencies="currencies"
      @input="selection_changed"
      v-model="selected_currency"
    ></currency-converter-selector>
    <p>
      <!-- TODO: SHOW CONVERTED PRICE TO 4 DECIMAL PLACES -->
      Price {{ selected_currency.name }}: ${{ getconvertedPrice() }}
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
    formatUsdPrice: function () {
      let num = Number(this.selected["priceUsd"]);
      this.selected["priceUsd"] = num.toFixed(4);
    },
    getconvertedPrice() {
      let price = this.selected["priceUsd"] * this.selected_currency["price"];
      price = price.toFixed(4);
      return price;
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
            "Something went wrong. Please try again"
          );
        });
    },
  },
  data() {
    return {
      crypto_data: undefined,
      converted_price: 0,
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