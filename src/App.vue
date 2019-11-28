<template lang="html">
  <div class="main-container">
    <beer-list :beers = "beers">  </beer-list>
    <beer-detail :beer = "selectedBeer"> </beer-detail>
    <div class="favourtie-container">
      <h2>you're favorites:</h2>
        <div v-for="(beer, index) in filtered" :beer ="beer">
        <li>{{beer}}</li>
          <button v-on:click="handleDelete(beer)"type="button" name="button">delete</button>
        </div>


      <!-- <p>{{favorites}}</p> -->
    </div>
  </div>
</template>

<script>
import BeerDetail from "./components/BeerDetail.vue"
import BeerList from "./components/BeerList.vue"
import SingleBeer from "./components/SingleBeer.vue"

import {eventBus} from "./main.js"
export default {
  name: "App",
  data(){
    return {
      beers: [],
      selectedBeer: null,
      favorites: [],
      beerToRemove: ""
      // filteredFavs: []
    }
  },
  mounted(){
    fetch("https://api.punkapi.com/v2/beers")
    .then(result => result.json())
    .then(beers => this.beers = beers)
    eventBus.$on("beer-favorite", beer => {this.favorites.push(beer['name'])})

    eventBus.$on("beer-selected", beer => {this.selectedBeer = beer})
  },
  computed:{
    filtered(){
      return this.favorites.filter((value, index, self) => self.indexOf(value) === index)
      }
  },
  components: {
    "beer-list": BeerList,
    "beer-detail": BeerDetail,
    "single-beer": SingleBeer
  },
  methods:{
    handleDelete(beer){
      this.favorites = this.favorites.filter( b => b!== beer)
    }
  }
}
</script>

<style lang="css" scoped>
 .main-container{
   display: flex;
   justify-content: space-between;
   width: 70%;

 }
</style>
