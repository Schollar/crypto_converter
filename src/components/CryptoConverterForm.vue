<template>
  <div>
    <form @submit.prevent="submit">
      <v-select
        return-object
        :items="crypto_data"
        item-text="name"
        label="Standard"
      ></v-select>
      <v-btn class="mr-4" type="submit" :disabled="invalid"> submit </v-btn>
      <v-btn @click="clear"> clear </v-btn>
    </form>
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
      items: [
        { name: "lol", price: 1 },
        { name: "poo", price: 2 },
        { name: "l", price: 3 },
        { name: "lo", price: 4 },
      ],
      crypto_data: undefined,
    };
  },
};
</script>

<style scoped>
</style>