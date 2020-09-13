<template>
  <div class="hello">
    
      <Country v-for="country in countries" :key="country.name" :country="country"/>


  </div>
</template>

<script>
import Country from './Country.vue'
export default {
  name: 'CountryList',
    components: {
    Country
  },
  props: [
    "countries"
  ],
  data() {
    return {

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
