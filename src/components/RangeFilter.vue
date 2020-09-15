<template>
  <div class="border-bottom p-1 m-1 mb-3">
    <h6 class="text-left ml-2 pb-4"><slot></slot></h6>
    <VueSimpleRangeSlider
      style="width: 300px"
      :min="minMax[0]"
      :max="minMax[1]"
      :logarithmic="true"
      v-model="range"
      @input="$emit('slider-changed', range)"
      barColor="#9d8d8f"
      activeBarColor="#faed26"
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
<style>
.simple-range-slider-popover {
  color: #d1bfbf;
}
</style>