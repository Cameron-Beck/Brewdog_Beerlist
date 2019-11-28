<template lang="html">
  <div class="main-container">
    <beer-list :beers = "beers">  </beer-list>
    <beer-detail :beer = "selectedBeer"> </beer-detail>
    <div class="favourtie-container">
      <h2>you're favorites:</h2>
      <li v-for="(beer, index) in favorites" :beer ="beer">{{beer}}</li>
      <!-- <p>{{favorites}}</p> -->
    </div>
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
      selectedBeer: null,
      favorites: []
    }
  },
  mounted(){
    fetch("https://api.punkapi.com/v2/beers")
    .then(result => result.json())
    .then(beers => this.beers = beers)

    eventBus.$on("beer-selected", beer => {this.selectedBeer = beer})
    eventBus.$on("beer-favorite", beer => {this.favorites.push(beer)})
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
