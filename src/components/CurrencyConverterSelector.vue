<template>
  <div>
    <v-select
      :items="currencies"
      label="Select a currency"
      v-model="selected"
      class="select"
      @input="change_selection()"
    ></v-select>
  </div>
</template>

<script>
export default {
  name: "currency-converter-selector",
  props: {
    currencies: Array,
  },
  data() {
    return {
      currency_data: undefined,
      selected: "",
    };
  },
  mounted() {
    this.get_currency_data();
  },
  methods: {
    change_selection() {
      let selected_currency = {
        name: this.selected,
        price: this.currency_data[this.selected.toLowerCase()],
      };
      this.$emit("input", selected_currency);
    },

    get_currency_data() {
      // Grabbing The prices of other currencies using USD as the base
      this.$axios
        .request({
          url: `https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies/usd.json`,
          method: "GET",
        })
        // Setting character tasks list to data sent back
        .then((response) => {
          this.currency_data = response.data.usd;
        })
        .catch((error) => {
          error;
          this.$root.$emit(
            "error_message",
            "Something went wrong please try again"
          );
        });
    },
  },
};
</script>

<style scoped>
</style>