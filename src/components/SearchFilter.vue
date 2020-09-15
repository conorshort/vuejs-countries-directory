<template>
  <div>

    <input
    id="search-input"
      v-model="text"
      @keyup="$emit('search-changed', text)"
      type="text"
      placeholder="Search for a country"
    />
  </div>
</template>

<script>
export default {
  name: "SearchFilter",
  props: [],
  data() {
    return {
      text: "",
    };
  },
  computed: {},
};
</script>

<style>
#search-input {
  background: #d1bfbf;
  color: #111111;
  width: 200px;
}
</style>