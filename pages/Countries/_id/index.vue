<template>
  <div class="nchi-info-main-container">
    <nuxt-link to="/countries" class="btn-back">&larr; Back</nuxt-link>
    <nuxt-link to="/" class="btn-back">&larr; Home</nuxt-link>

    <div v-for="currentInfo in countryInfo" v-bind:key="currentInfo.alpha3Code" class="country-info-container">

      <div class="country-img">
        <img v-bind:src="currentInfo.flag">
      </div>

      <div class="country-info">
        <ul class="country-info__stats--premiere">
          <li>{{$route.params.id}}</li>
          <li>Native Name: {{currentInfo.nativeName}}</li>
          <li>Population: {{currentInfo.population}}</li>
          <li>Region: {{currentInfo.region}}</li>
          <li>Sub-region: {{currentInfo.subRegion}}</li>
          <li>Capital City: {{currentInfo.capital}}</li>
        </ul>

        <div class="country-info__stats--deuxieme">
          <div class="test" v-if="currentInfo.topLevelDomain">
            <span v-for="(currentDomain, index) in currentInfo.topLevelDomain" v-bind:key="index">
              Top Level Domain: {{currentDomain}}
            </span>
          </div>
          <div v-if="currentInfo.currencies">
            <span v-for="(currentCurrency, index) in currentInfo.currencies" v-bind:key="index">
              Currency: {{currentCurrency.name}}
            </span>
          </div>
          <div v-if="currentInfo.languages">
            <span>Language(s): </span>
            <ul v-for="(currentLanguage, index) in currentInfo.languages" v-bind:key="index">
              <li>{{currentLanguage.name}}</li>
              <li>{{currentLanguage.nativeName}}</li>
            </ul>
          </div>
        </div>
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

<style lang="scss">
.nchi-info-main-container {
  max-width: 114rem;
  margin: 4rem auto;
  overflow: hidden;
}

.country-info-container {
  display: grid;
  grid-template-columns: repeat(12, minmax(8.5rem, 1fr));
  //   grid-template-rows: repeat(2, minmax(min-content, 1fr));
  grid-template-rows: 1fr;
  margin-top: 2.5rem;
  gap: 1.5rem;
}

.country-info {
  //   grid-row: 2 / -1;
  grid-column: 6/-1;
  display: grid;
  grid-template-columns: subgrid;

  ul {
    list-style: none;
  }

  &__stats {
    &--premiere {
      grid-column: 1 / 4;
    }

    &--deuxieme {
      grid-column: 4 / -1;
    }
  }

  //   &__infostats1 {
  //     grid-column: 1 / 4;
  //   }

  //   &__infostats2 {
  //     grid-column: 1 / 4;
  //   }
}

.country {
  &-img {
    grid-column: 1 / 6;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
  &-info {
    // grid-column: 6/-1;
  }
}
</style>