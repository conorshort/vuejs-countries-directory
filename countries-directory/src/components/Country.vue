<template>
  <div class="country-box" @click="toggleShowInfo">
    <div>
      <b-card :title="country.name">
        <!-- <b-card-title> -->
        <b-card-text v-show="showInfo">
          <img :src="country.flag" :alt="country.name + ' flag'" height="50" />
          <b>Region:</b>
          {{ country.region }}
          <b>Population:</b>
          {{ country.population }}
          <b>Capital:</b>
          {{ country.capital }}
        </b-card-text>
      </b-card>
    </div>
  </div>
</template>

<script>
export default {
  name: "Country",
  props: ["country"],
  data() {
    return {
      showInfo: false,
    };
  },
  methods: {
    toggleShowInfo() {
      this.showInfo = !this.showInfo;
    },
  },
};
</script>

<style>
.country-box {
  width: 600px;
  margin: auto;
}
</style>