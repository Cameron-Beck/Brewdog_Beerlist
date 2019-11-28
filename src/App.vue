<template lang="html">
  <div class="main-container">
    <beer-list :beers = "beers">  </beer-list>
    <beer-detail :beer = "selectedBeer"> </beer-detail>
  </div>
</template>

<script>
import BeerDetail from "./components/BeerDetail.vue"
import BeerList from "./components/BeerList.vue"

import {eventBus} from "./main.js"
export default {
  name: "App",
  data(){
    return {
      beers: [],
      selectedBeer: null
    }
  },
  mounted(){
    fetch("https://api.punkapi.com/v2/beers")
    .then(result => result.json())
    .then(beers => this.beers = beers)

    eventBus.$on("beer-selected", beer => {this.selectedBeer = beer})
  },
  components: {
    "beer-list": BeerList,
    "beer-detail": BeerDetail
  }
}
</script>

<style lang="css" scoped>
 .main-container{
   display: flex;
   justify-content: space-between;
 }
</style>
