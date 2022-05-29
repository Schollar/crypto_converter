<template>
  <div class="footer_container">
    <section class="info_container">
      <p>
        The currency data is only updated once a day so it may not reflect the
        same prices as a real time service provides.<br />
        *The API service used for currency data is located
        <span
          ><a
            href="https://github.com/fawazahmed0/currency-api#readme"
            target="__blank"
            >here</a
          > </span
        ><br />
        If you would like to donate so I am able to upgrade to a live service
        you can do so
        <span
          ><a href="https://paypal.me/schollar4" target="__blank">here</a></span
        >
      </p>
    </section>
  </div>
</template>

<script>
export default {
  name: "page-footer",
};
</script>

<style lang="scss" scoped>
.footer_container {
  margin-top: 30%;
  color: #598392;
}
.info_container {
  display: grid;
  place-items: center;

  > p {
    width: 80%;
    font-size: 0.8em;
  }
}
</style>