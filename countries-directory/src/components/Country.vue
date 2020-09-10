<template>
  <div class="country-box" @click="toggleShowInfo">
    <h2>{{ country.name }} <img :src="country.flag" :alt="country.name + ' flag'" width="30" height="20"></h2>
    <div v-show="showInfo">
      <p>
        <b>Region:</b>
        {{ country.region }}
      </p>
      <p>
        <b>Population:</b>
        {{ country.population }}
      </p>
      <p>
        <b>Capital:</b>
        {{ country.capital }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Country",
  props: ["country"],
  data(){
      return {
          showInfo: false
      }
  },
  methods: {
      toggleShowInfo() {
          this.showInfo = !this.showInfo
      }
  }
}
</script>

<style>
.country-box {
  border-style: groove;
  width: 600px;
  margin: auto;
}
</style>