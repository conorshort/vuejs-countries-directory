<template>
  <div>
    <label>Select region</label>
    <multiselect
      v-model="value"
      :options="options"
      :multiple="true"
      :close-on-select="false"
      :clear-on-select="false"
      :preserve-search="true"
      placeholder="Pick some"
      :preselect-first="true"
      @input="$emit('dropdown-updated', value)"
    >
      <template slot="selection" slot-scope="{ values, isOpen }">
        <span
          class="multiselect__single"
          v-if="values.length &amp;&amp; !isOpen"
        >{{ values.length }} options selected</span>
      </template>
    </multiselect>
  </div>
</template>

<script>
import Multiselect from "vue-multiselect";

export default {
  components: {
    Multiselect,
  },
  props: ["optionsList"],
  data() {
    return {
      value: [],
      options: [],
    };
  },
  watch: {
    // whenever question changes, this function will run
    optionsList: function (newOptions) {
      this.options =newOptions
      //this.$emit('slider-changed', this.range)
    },
  },
};
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

<style>
</style>