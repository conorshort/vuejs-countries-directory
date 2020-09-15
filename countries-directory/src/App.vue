<template>
  <div id="app">
    <div>
      <b-navbar toggleable="lg" type="dark" id="navbar" variant="nav">
        <b-navbar-brand id="navbar-title">Countries Directory</b-navbar-brand>
      </b-navbar>
    </div>
    <b-container fluid class="p-0">
      <b-row no-gutters>
        <b-col cols="12" md="5" class>
          <b-button class="mb-2 d-md-none" block variant="outline-accent" @click="showFilters = ! showFilters">
            Show Filters
            <b-icon
              :icon="! showFilters ? 'chevron-compact-down' : 'chevron-compact-up'"
              aria-hidden="true"
            ></b-icon>
          </b-button>
          <div
            class="border-right p-2 dark-background"
            id="filter-div"
            :class="showFilters ? '' : 'zero-height'"
          >
            <h4 class="text-left m-3">Filters:</h4>
            <range-filter @slider-changed="updatePopRange" :minMax="minMaxPop">Population:</range-filter>
            <range-filter @slider-changed="updateAreaRange" :minMax="minMaxArea">Area:</range-filter>
            <dropdown-filter
              @dropdown-updated="updateSelectedRegions"
              :optionsList="allRegions"
            >Region:</dropdown-filter>
          </div>
        </b-col>
        <b-col cols="12" md="7" id="countries-col">
          <div class="countries-div">
            <b-row
              align-v="center"
              align-h="start"
              class="mt-0 mb-5 p-3 border-bottom light-background"
            >
              <b-col cols="12" md="4">
                <search-filter @search-changed="updateSearchText" />
              </b-col>
              <b-col cols="12" md="8">
                <sort-buttons @input="sortCountries" />
              </b-col>
            </b-row>
            <b-row>
              <b-col>
                <CountryList :countries="filteredCountries" />
              </b-col>
            </b-row>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import CountryList from "./components/CountryList.vue";
import SearchFilter from "./components/SearchFilter.vue";
import RangeFilter from "./components/RangeFilter.vue";
import DropdownFilter from "./components/DropdownFilter.vue";
import SortButtons from "./components/SortButtons.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    CountryList,
    SearchFilter,
    RangeFilter,
    DropdownFilter,
    SortButtons,
  },
  data() {
    return {
      countries: [],
      alphaCountries: [],
      searchText: "",
      minMaxPop: [],
      minMaxArea: [],
      popRange: [],
      areaRange: [],
      allRegions: [],
      selectedRegions: [],
      showFilters: false
    };
  },
  computed: {
    filteredCountries() {
      let filteredArray = this.countries.filter(this.countryStartsWith);
      filteredArray = filteredArray.filter(this.countryPopulationInRange);
      filteredArray = filteredArray.filter(this.countryAreaInRange);
      filteredArray = filteredArray.filter(this.countryInRegion);
      return filteredArray;
    },
  },
  methods: {
    sortCountries(keyToSortBy, isReversed) {
      let countries = this.alphaCountries;

      countries.sort((a, b) => {
        let aVal = a[keyToSortBy];
        let bVal = b[keyToSortBy];

        if (typeof aVal == "string" && typeof bVal == "string") {
          return aVal.localeCompare(bVal);
        } else {
          return aVal - bVal;
        }
      });
      if (isReversed) {
        countries = countries.reverse();
      }
      this.countries = countries;
    },

    updateSearchText(text) {
      this.searchText = text;
    },
    updatePopRange(range) {
      this.popRange = range;
    },
    updateAreaRange(range) {
      this.areaRange = range;
    },
    updateSelectedRegions(regions) {
      this.selectedRegions =
        regions && regions.length ? regions : this.allRegions;
    },
    countryStartsWith(country) {
      let countryName = country.name.toLowerCase();
      return countryName.startsWith(this.searchText.toLowerCase());
    },
    countryPopulationInRange(country) {
      let population = country.population;
      return this.popRange[0] <= population && population <= this.popRange[1];
    },
    countryAreaInRange(country) {
      let area = country.area;
      return this.areaRange[0] <= area && area <= this.areaRange[1];
    },
    countryInRegion(country) {
      let region = country.region;
      return this.selectedRegions.includes(region);
    },

    getMinMax() {
      let maxPop = this.countries[0].population;

      let maxArea = this.countries[0].area;

      for (let i = 1, len = this.countries.length; i < len; i++) {
        let p = this.countries[i].population;
        maxPop = p > maxPop ? p : maxPop;

        let a = this.countries[i].area;
        maxArea = a > maxArea ? a : maxArea;
      }

      return { pop: [0, maxPop], area: [0, maxArea] };
    },
    getAllRegions() {
      let allRegions = [];
      this.countries.forEach((country) => {
        if (!allRegions.includes(country.region)) {
          allRegions.push(country.region);
        }
      });
      return allRegions;
    },
  },
  created() {
    axios.get("https://restcountries.eu/rest/v2/all").then((response) => {
      this.countries = response.data;
      this.alphaCountries = [...this.countries];
      this.alphaCountries.sort((a, b) => a.name.localeCompare(b.name));
      let pop, area;
      ({ pop, area } = this.getMinMax());
      this.minMaxPop = pop;
      this.minMaxArea = area;
      this.popRange = pop;
      this.areaRange = area;

      this.allRegions = this.getAllRegions();
      this.selectedRegions = [...this.allRegions];
    });
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Nunito&display=swap");
#app {
  font-family: Nunito, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #9d8d8f;
  background-color: #514e52;
}
#countries-col {
  height: calc(100vh - 56px);
  overflow-y: scroll;
}

#navbar-title {
  color: #2c3e50;
}

.dark-background {
  background: #514e52;
}
.light-background {
  background: #514e52;
}

#filter-div {
  height: 100%;
}
 @media only screen and (max-width: 768px) {
    .zero-height{
    height: 0px;
    overflow: hidden;
  }
}
</style>
