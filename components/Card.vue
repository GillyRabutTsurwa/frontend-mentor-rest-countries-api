<template>
  <div class="card">
    <div class="card__country">
      <img v-bind:src="countryObj.flag" alt="">
    </div>
    <div class="card__info">
      <h5 class="card__info--title">{{countryObj.name}}</h5>
      <div class="card__info-section">
        <span class="card__info--subtitle">Population</span>: <span class="card__info--data">{{countryObj.population}}</span>
      </div>
      <div class="card__info-section">
        <span class="card__info--subtitle">Region</span>: <span class="card__info--data">{{countryObj.region}}</span>
      </div>
      <div class="card__info-section">
        <span class="card__info--subtitle">Capital</span>: <span class="card__info--data">{{countryObj.capital}}</span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "@nuxtjs/axios";
export default {
  props: {
    countryObj: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="scss">
.card {
  width: 30rem;
  height: 40rem;
  border-radius: 1rem;

  display: flex;
  //   A cause de column: basis in lines below = height, NOT width
  flex-direction: column;
  //   alignitems va pas affecter l'image (comme desiree) car il prend 100% de son parent
  // En fait, centraliser c'est trop d'espece
  //   align-items: center;
  overflow: hidden;

  box-shadow: 0 1rem 0.5rem rgba(0, 0, 0, 0.2);

  &__country {
    flex: 0 0 40%;
    img {
      width: 100%;
      height: 100%;
    }
  }
  &__info {
    &-section {
      margin-bottom: 0.75rem;
    }

    flex: 0 0 60%;
    margin: 2rem 0 0 2rem;

    &--title {
      font-size: 2rem;
      margin-bottom: 1.5rem;
    }

    &--subtitle {
      font-weight: bold;
    }
  }
}
</style>