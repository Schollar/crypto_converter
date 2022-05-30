<template>
  <section class="alert">
    <v-alert color="red" dismissible :value="error_alert" type="error">
      {{ error_message }}
    </v-alert>
  </section>
</template>

<script>
export default {
  name: "toast-notification",
  data() {
    return {
      error_message: "",
      error_alert: false,
    };
  },
  // Listening for the global event api message which is sent on every axios request error, and we call the show message function
  mounted() {
    this.$root.$on("error_message", this.show_error);
  },
  methods: {
    show_error: function (string) {
      this.error_message = string;
      this.error_alert = true;
      setInterval(() => {
        this.error_alert = false;
      }, 3000);
    },
  },
};
</script>

<style lang="scss" scoped>
.alert {
  width: 80%;
  position: absolute;
  top: 80vh;
  left: 10%;

  z-index: 2;
}
</style>