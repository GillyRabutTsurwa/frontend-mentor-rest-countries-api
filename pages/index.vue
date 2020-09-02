<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">
        <a href="https://www.frontendmentor.io/challenges/rest-countries-api-with-color-theme-switcher-5cacc469fec04111f7b848ca" target="_blank">Rest Countries API</a>
      </h1>
      <div class="links">
        <a href="https://restcountries.eu/#api-endpoints-name" target="_blank" rel="noopener noreferrer" class="button--green">
          API Link
        </a>
        <nuxt-link to="/all" class="button--green">
          All Countries
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
// TESTING: Axios fetching requests
import axios from "@nuxtjs/axios";
export default {
  async created() {
    const response = await this.$axios.$get(
      "https://restcountries.eu/rest/v2/all"
    );
    console.log(response);
  },
};
</script>

<style lang="scss">
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;

  a {
    text-decoration: none;
    color: #35495e;
  }
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
