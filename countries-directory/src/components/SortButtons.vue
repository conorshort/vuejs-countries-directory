<template>
  <div>
    <b-form-group label="Sort by:">
      <b-form-radio-group
        id="btn-radios-1"
        v-model="selected"
        :options="options"
        buttons
        name="radio-btn-outline"
        button-variant="outline-danger"
        size="lg"
        @input="$emit('input', selected, isReversed) "
      ></b-form-radio-group>
      <b-button size="lg" variant="outline-danger" class="ml-2" @click="toggleReversed">
        <b-icon icon="arrow-down-up" aria-label="Help"></b-icon>
      </b-button>
    </b-form-group>
  </div>
</template>

<script>
export default {
  data() {
    return {
        selected: "name",
        isReversed: false
    };
  },
  methods : {
      toggleReversed () {
          this.isReversed = !this.isReversed
          this.$emit('input', this.selected, this.isReversed) 
      }
  },
  computed: {
      options() {
        let alphaSortString, numSortString
        if (! this.isReversed){
            alphaSortString = "(A - Z)"
            numSortString = "(Low - High)"
        } else  {
            alphaSortString = "(Z - A)"
            numSortString = "(High - Low)"
        }
        
        return [
            { text: "Name "+ alphaSortString, value: "name" },
            { text: "Area " + numSortString, value: "area" },
            { text: "Population " + numSortString, value: "population" },
        ]

      }
  }
};
</script>