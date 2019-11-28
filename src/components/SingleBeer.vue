<template lang="html">
  <li v-on:click="handleClick" :value="beer">{{beer.name}}</li>
</template>

<script>
import {eventBus} from "../main.js"
export default {
  name: "single-beer",

  props: ["beer"],

  methods: {
    handleClick(){
      eventBus.$emit("beer-selected", this.beer)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
