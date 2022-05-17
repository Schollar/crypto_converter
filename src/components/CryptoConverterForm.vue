<template>
  <div>
    <form class="crypto_form">
      <v-select
        return-object
        :items="crypto_data"
        item-text="name"
        label="Standard"
        v-model="selected"
        class="select"
      ></v-select>
    </form>
    <p>{{ selected.priceUsd }}</p>
  </div>
</template>

<script>
export default {
  name: "crypto-converter",
  mounted() {
    this.get_crypto_data();
  },
  methods: {
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
      selected: "Select a Coin first!",
    };
  },
};
</script>

<style scoped>
.crypto_form {
  border: 1px solid black;
}
</style>