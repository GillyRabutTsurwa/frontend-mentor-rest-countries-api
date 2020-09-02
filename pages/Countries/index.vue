<template>
  <div class="card-container">
    <Card v-for="currentPaysObj in tousLesPays" v-bind:key="currentPaysObj.alpha3Code" v-bind:countryObj="currentPaysObj" />
  </div>
</template>

<script>
import axios from "@nuxtjs/axios";
import Card from "~/components/Card";
export default {
  data() {
    return {
      tousLesPays: [],
    };
  },
  components: {
    Card: Card,
  },
  async created() {
    const response = await this.$axios.$get(
      "https://restcountries.eu/rest/v2/all"
    );
    // console.log(response);
    this.tousLesPays = response;
    console.log(this.tousLesPays);
  },
};
</script>

<style lang="scss">
.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(30rem, 35rem));
  gap: 3rem;
  justify-content: center;
}
</style> 