<template>
  <div id="app">
    <div id="container">
    <div class="navigation">
      <button v-on:click="toggleDark">☀️/🌙</button>
    <search-form @search:country="searchCountry" v-bind:all-countries="allCountries"/>


    <div v-if="manyResults">
    <result-selection @select:country="selectCountry" v-bind:result="result"/>
    </div>
    </div>
    <div id="main-info">
    <div id="one-result" v-if="oneResult">
      <big-result v-bind:country="country"  v-bind:allCountries="allCountries"/>
    </div>
      <div id="source-link">
        <a href="https://github.com/AndreasMeier12/countrywebgui">Source</a>
      </div>


    </div>


    </div>
  </div>
</template>

<script>
import SearchForm from './components/SearchForm.vue'
import ResultSelection from './components/ResultSelection.vue'
import BigResult from './components/BigResult.vue'

export default {
  name: 'App',
  components: {
    ResultSelection,
    SearchForm,
    BigResult,
  },
  methods: {
    searchCountry(result) {
      this.country = null;
      this.result = result;
      if (result.length == 1) {
        this.oneResult = true;
        this.country = result[0];
      }
      if (result.length > 1) {
        this.manyResults = true;
      }



    },
    selectCountry(country){
      this.oneResult=true;
      this.country = this.result.filter(a => a['name']===country)[0];
    },
    async prefetch(){
      const url = 'https://restcountries.eu/rest/v2/all';
      const response = await fetch(url);
      this.allCountries = await response.json();
    },
    toggleDark(){
      console.log("dork")
      this.theme = this.theme === 'darkMode' ? '' : 'darkMode'; //toggles theme value
      document.documentElement.setAttribute('data-theme', this.theme); // sets the data-theme attribute
      localStorage.setItem('theme', this.theme); // stores theme value on local storage

    }

  },
  data() {
    return {
      result: '',
      oneResult: false,
      manyResults: false,
      country: null,
      allCountries : {},
      theme: '',
    }
  },
  mounted() {
    this.prefetch();

  }
}
</script>

<style>
  @import "assets/styles/light.css";
  @import "assets/styles/shared.css";

  #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
