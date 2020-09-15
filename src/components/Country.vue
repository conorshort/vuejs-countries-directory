<template>
  <div class="country-box" @click="toggleShowInfo">
    <div class="hover-bg">
      <b-card class="mb-2" >
        <h4 class="mt-0 pb-2 mb-4 country-heading border-bottom">{{country.name}}</h4>
        <b-media>
          <template v-slot:aside>
            <b-img class="ml-5 mt-2 shadow" :src="country.flag" width="120" alt="placeholder"></b-img>
          </template>
          <b-row align-h="end">
            <b-col cols="8" class="country-initial-info">
              <p>
                <b>Region:</b>
                {{ country.region }}
              </p>
              <p>
                <b>Population:</b>
                {{ country.population }}
              </p>
              <p>
                <b>Area:</b>
                {{ country.area }}
              </p>
            </b-col>
          </b-row>
        </b-media>
        <b-button class="mb-2" block variant="primary-outline">
          <b-icon
            :icon="! showInfo ? 'chevron-compact-down' : 'chevron-compact-up'"
            aria-hidden="true"
          ></b-icon>
        </b-button>
        <b-collapse id="collapse-1" class="mt-2" v-model="showInfo">
          <b-row>
            <b-col cols="6">
              <p>
                <b>Timezone:&nbsp;</b>
                  <span v-for="(tzone, idx) in country.timezones" :key="idx"><span v-if="idx != 0">, </span>{{tzone.trim()}}</span>
              </p>
              <p>
                <b>Languages:&nbsp;</b>
                <span v-for="(lang, idx) in country.languages" :key="idx"><span v-if="idx != 0">, </span>{{lang.name.trim()}}</span>
              </p>

            </b-col>
            <b-col cols="6">
                            <p>
                <b>Currencies:&nbsp;</b>
                <span v-for="(curr, idx) in country.currencies" :key="idx"><span v-if="idx != 0">, </span>{{curr.name.trim()}}</span>
              </p>
              <p>
                <b>Capital:</b>
                {{ country.capital }}
              </p>
            </b-col>
          </b-row>
        </b-collapse>
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

<style scoped>
.country-box {
  width: 600px;
  margin: auto;
}
.card {
  color: #111111;
  background-color: #9d8d8f;
  transition: 0.2s;
}

.card:hover {
  background-color: #d1bfbf;
}

.country-initial-info {
  text-align: left;
}
</style>