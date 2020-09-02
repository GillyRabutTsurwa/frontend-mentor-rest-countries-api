<template>
  <div class="container">
    <div>
      <!-- <Logo /> -->

      <div class="main-page-img">
        <transition name="fade" mode="out-in">
          <img v-bind:src="currentFlag" v-bind:key="currentFlag" alt="">
        </transition>
      </div>
      <h1 class="title">
        <a href="https://www.frontendmentor.io/challenges/rest-countries-api-with-color-theme-switcher-5cacc469fec04111f7b848ca" target="_blank">Rest Countries API</a>
      </h1>
      <div class="links">
        <a href="https://restcountries.eu/#api-endpoints-name" target="_blank" rel="noopener noreferrer" class="button--green">
          API Link
        </a>
        <nuxt-link to="/countries" class="button--green">
          All Countries
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "@nuxtjs/axios";
export default {
  data() {
    return {
      currentIndex: null,
      flagsArr: [],
    };
  },
  methods: {
    randomiseIndex() {
      this.currentIndex = Math.floor(Math.random() * this.flagsArr.length);
    },
    startFadingImages() {
      this.randomiseIndex();
      setInterval(this.randomiseIndex, 6000);
    },
  },
  async created() {
    const response = await this.$axios.$get(
      "https://restcountries.eu/rest/v2/all"
    );

    this.flagsArr = response.map((currentData) => currentData.flag);
    console.log(this.flagsArr);
  },
  mounted() {
    // setInterval(this.randomiseIndex, 6000);
    this.startFadingImages();
  },
  computed: {
    currentFlag() {
      return this.flagsArr[this.currentIndex];
    },
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
  font-weight: bold;
  font-size: 6rem;
  color: #35495e;
  letter-spacing: 1px;
  text-transform: uppercase;

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

.main-page-img {
  width: 50rem;
  height: 30rem;
  box-shadow: 0 1rem 1rem rgba(0, 0, 0, 0.4);
  margin: 0 auto;

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    // TESTING:
    position: relative;
  }
}

.fade-enter-active {
  transition: opacity 5s ease-in;
  // transition-delay: 1s;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 2s ease-in;
  opacity: 1;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
