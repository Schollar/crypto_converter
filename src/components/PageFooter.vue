<template>
  <div class="footer_container">
    <section class="info_container">
      <p>
        *The API service used for currency data is located
        <span
          ><a
            href="https://github.com/fawazahmed0/currency-api#readme"
            target="__blank"
            >here</a
          ><br />
        </span>
      </p>
      <p>
        **The currency data is only updated
        <span class="bold">once a day</span> so it may not reflect the same as a
        real time service price.<br />
      </p>
      <p>
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
  margin-top: 20%;
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
.bold {
  font-weight: bolder;
}
</style>