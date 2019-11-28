<template lang="html">
  <ul>
    <single-beer v-for="(beer, index) in beers" :beer ="beer" :key ="index">{{beer.name}}</single-beer>
  </ul>
</template>

<script>
import SingleBeer from "./SingleBeer.vue";
export default {
  name: "beer-list",

  props: ["beers"],

  components:{
    "single-beer": SingleBeer
  }
}
</script>

<style lang="css" scoped>
</style>
