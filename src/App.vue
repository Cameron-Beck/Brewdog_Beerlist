<template lang="html">
  <div class="main-container">

    <div class="container1">
        <h1>All Beers</h1>
    <beer-list class="beer-list"  :beers = "beers">  </beer-list>
    </div>

    <beer-detail class="container3" :beer = "selectedBeer"> </beer-detail>

    <div class="container2">
      <h2>Your Favorites:</h2><br>
        <div v-for="(beer, index) in filtered" :beer ="beer">
        <li>{{beer}}</li>
          <button v-on:click="handleDelete(beer)"type="button" name="button">delete</button>
        </div>
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
  flex-wrap: wrap;
  width: 100%;
  justify-content: space-between;
}

 .container1{
   display: flex;
   /* justify-content: space-between; */
   background-color: #DEF3FD;
   flex-direction: column;
   width: 30%;
   align-items: center;
   align-items: center;
   border-radius: 5%;
   padding: 10px;

 }
.container1:hover{
  box-shadow: -1px 10px 29px 0px rgba(0,0,0,0.8);
}

 .container2{
   display: flex;
   /* justify-content: space-between; */
   background-color: #FCF7DE  ;
   flex-direction: column;
   width: 30%;
   align-items: center;
   align-items: center;
   border-radius: 5%;
   font-size: 25px;
   padding: 10px;
 }

 .container2:hover{
   box-shadow: -1px 10px 29px 0px rgba(0,0,0,0.8);
 }
 .container3{
   /* justify-content: space-between; */
   display: flex;
   background-color: #FDDFDF;
   flex-direction: column;
   width: 30%;
   align-items: center;
   border-radius: 5%;
   padding: 10px;
 }

 .container3:hover{
   box-shadow: -1px 10px 29px 0px rgba(0,0,0,0.8);
 }

.beer-list{
     text-decoration: none;

}


</style>
