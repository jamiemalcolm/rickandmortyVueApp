<template>
  <div>
    <li v-on:click="handleLocationClick">{{ location.name }}</li>
  </div>
</template>

<script>
import { eventBus } from "../main.js";
export default {
  name: "location",
  props: ["location"],
  methods: {
    handleLocationClick: function () {
      eventBus.$emit("selected-location", this.location);
    },
  },
};
</script>

<style>
</style>