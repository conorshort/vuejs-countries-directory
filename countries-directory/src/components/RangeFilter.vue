<template>
  <div>
    <VueSimpleRangeSlider
      style="width: 300px"
      :min="minMax[0]"
      :max="minMax[1]"
      :logarithmic="true"
      v-model="range"
      @input="$emit('slider-changed', range)"
    />
  </div>
</template>
<script>
import VueSimpleRangeSlider from "vue-simple-range-slider";
import "vue-simple-range-slider/dist/vueSimpleRangeSlider.css";
export default {
  // register the component
  components: { VueSimpleRangeSlider },
  props: ["minMax"],
  data() {
    return {
      range: [],
    };
  },
  watch: {
    // whenever question changes, this function will run
    minMax: function (newMinMax) {
      this.range = [...newMinMax]
      //this.$emit('slider-changed', this.range)
    },
  },
};
</script> 