<template lang="html">
  <div v-if="beer">
    <h3>Beer Name: {{beer.name}}</h3>
    <p>Description: {{beer.description}}</p>
    <p>tagline: {{beer.tagline}}</p>
    <p>ABV: {{beer.abv}}</p>
    <img :src="beer.image_url" alt="">

  </div>
</template>

<script>
import {eventBus} from "../main.js"
export default {
  name: "beer-detail",

  props: ['beer']

}
</script>

<style lang="css" scoped>
</style>
