<template>

  <div id="app">
    <div>
  <b-navbar toggleable="lg" type="dark" variant="info">
    <b-navbar-brand href="#">Countries Directory</b-navbar-brand>
  </b-navbar>
</div>
    <CountryList :countries="countries" />
  </div>
</template>

<script>
import CountryList from "./components/CountryList.vue";
import axios from 'axios'

export default {
  name: "App",
  components: {
    CountryList,
  },
  data() {
    return {
      countries: [],
    };
  },
  created() {
    axios
        .get("https://restcountries.eu/rest/v2/all")
        .then((response) => (this.countries = response.data));
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
