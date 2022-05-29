<template>
  <div class="heading_container">
    <h1>Coin Price</h1>
    <p>Check prices of different Crypto coins in different currencies.</p>
  </div>
</template>

<script>
export default {
  name: "page-header",
};
</script>

<style lang="scss" scoped>
.heading_container {
  margin-top: 5%;
  display: grid;
  place-items: center;
  width: 100%;
  text-align: center;
  color: #598392;
  font-family: "Lato", sans-serif;
  > h1 {
    font-size: 3rem;
  }
  > p {
    max-width: 80%;
  }
}
</style>