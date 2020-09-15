<template>
  <div class="bg">
    <b-button-toolbar key-nav>
      <b-form-radio-group
        id="btn-radios-1"
        v-model="selected"
        :options="options"
        buttons
        name="radio-btn-outline"
        button-variant="outline-accent"
        size="sm"
        @input="$emit('input', selected, isReversed) "
        class="hello"
      ></b-form-radio-group>
      <b-button-group>
        <b-button size="sm" variant="outline-accent" class="ml-2" @click="toggleReversed">
          <b-icon icon="arrow-down-up" aria-label="Help"></b-icon>
        </b-button>
      </b-button-group>
    </b-button-toolbar>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selected: "name",
      isReversed: false,
    };
  },
  methods: {
    toggleReversed() {
      this.isReversed = !this.isReversed;
      this.$emit("input", this.selected, this.isReversed);
    },
  },
  computed: {
    options() {
      let alphaSortString, numSortString;
      if (!this.isReversed) {
        alphaSortString = "(A - Z)";
        numSortString = "(Low - High)";
      } else {
        alphaSortString = "(Z - A)";
        numSortString = "(High - Low)";
      }

      return [
        { text: "Name " + alphaSortString, value: "name" },
        { text: "Area " + numSortString, value: "area" },
        { text: "Population " + numSortString, value: "population" },
      ];
    },
  },
};
</script>

<style lang="scss">
// .bg {
//   background: $blue;
// }

/* .btn-outline-danger {
  color: #faed26 !important;
  background-color: #46344e !important;
  border-color: #faed26 !important;
}

.btn-outline-danger:hover {
  color: #46344e !important;
  background-color: #faed26 !important;
  border-color: #faed26 !important;
}
 */


</style>