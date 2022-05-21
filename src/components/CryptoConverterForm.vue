<template>
  <div class="form_container">
    <form class="crypto_form">
      <v-select
        return-object
        :items="crypto_data"
        item-text="name"
        label="Select a coin"
        v-model="selected"
        class="select"
      ></v-select>
      <p>Price USD: ${{ formatUsdPrice() }}</p>
      <currency-converter-selector
        :currencies="currencies"
        v-model="selected_currency"
      ></currency-converter-selector>
      <p>Price {{ selected_currency.name }}: ${{ getconvertedPrice() }}</p>
    </form>
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
    formatUsdPrice() {
      if (this.selected.priceUsd === 0) {
        return 0;
      } else {
        let num = Number(this.selected["priceUsd"]);
        num = num.toFixed(4);
        return num;
      }
    },
    getconvertedPrice() {
      if (this.selected_currency.price === 0) {
        return 0;
      } else {
        let price = this.selected["priceUsd"] * this.selected_currency["price"];
        price = price.toFixed(4);
        return price;
      }
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
        name: "",
        price: 0,
      },
    };
  },
};
</script>

<style scoped>
.form_container {
  display: grid;
  place-items: center;
  margin-top: 10%;
  margin-bottom: 10%;
}
.crypto_form {
  padding: 20px;
  border: 1px solid black;
  border-radius: 15px;
}
</style>