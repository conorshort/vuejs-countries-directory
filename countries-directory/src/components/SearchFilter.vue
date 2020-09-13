<template>
    <input v-model="text" @keyup="$emit('search-changed', text)" type="text" placeholder="Search for a country">
</template>

<script>
export default {
  name: 'SearchFilter',
  props: [
 
  ],
  data() {
      return {
          text: ""
      }
  },
  computed: {

  }
}

</script>

<style>

</style>