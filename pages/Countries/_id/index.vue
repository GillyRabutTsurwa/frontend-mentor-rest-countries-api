<template>
  <div>

    <h5>{{$route.params.id}}</h5>
    <!--   -->
    <!-- <h6> {{countryInfo[0].nativeName}} </h6> -->
    <div v-for="currentInfo in countryInfo" v-bind:key="currentInfo.alpha3Code">
      <h6>{{currentInfo.nativeName}}</h6>
      <h6>{{currentInfo.population}}</h6>
      <h6>{{currentInfo.region}}</h6>
      <h6>{{currentInfo.subRegion}}</h6>
      <h6>{{currentInfo.capital}}</h6>
      <div v-if="currentInfo.topLevelDomain">
        <h6 v-for="(currentDomain, index) in currentInfo.topLevelDomain" v-bind:key="index">
          {{currentDomain}}
        </h6>
      </div>
      <div v-if="currentInfo.currencies">
        <h6 v-for="(currentCurrency, index) in currentInfo.currencies" v-bind:key="index">
          {{currentCurrency.name}}
        </h6>
      </div>
      <div v-if="currentInfo.languages">
        Language(s)
        <h6 v-for="(currentLanguage, index) in currentInfo.languages" v-bind:key="index">
          <span>{{currentLanguage.name}}</span> -
          <span>{{currentLanguage.nativeName}}</span>
        </h6>
      </div>
    </div>
  </div>

</template>

<script>
import axios from "@nuxtjs/axios";

export default {
  data() {
    return {
      // NOTE: Bien que ce soit juste une chose dans le tableau, néanmoins, c'est un tableau.
      //   A cause de ca, je vais utiliser [0] pour obtenir les info plutot de looper.
      // Jussskidding. Je vais looper. Ca marche pas sans le boucle
      countryInfo: [],
    };
  },
  async created() {
    const response = await this.$axios.$get(
      `https://restcountries.eu/rest/v2/name/${this.$route.params.id}`
    );
    console.log(response);
    this.countryInfo = response;
    console.log(this.countryInfo);
  },
};
</script>

<style>
</style>