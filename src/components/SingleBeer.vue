<template lang="html">
  <div>
  <li v-on:click="handleClick" :value="beer">{{beer.name}}</li>
  <button  class="add-favorite" v-on:click="handleFavouriteAdd" :value="beer">Add to favourites</button>
  </div>
</template>

<script>
import {eventBus} from "../main.js"
export default {
  name: "single-beer",

  props: ["beer"],

  methods: {
    handleClick(){
      eventBus.$emit("beer-selected", this.beer)
    },
    handleFavouriteAdd(){
      eventBus.$emit("beer-favorite", this.beer)
    }
  }
}
</script>

<style lang="css" scoped>
.add-favorite{
  display: block;
  width: 70px;
  height: 30px;
  
}
</style>
