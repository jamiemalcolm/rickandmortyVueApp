<template>
  <div>
    <li v-on:click="handleNameClick">{{ character.name }}</li>
  </div>
</template>

<script>
import { eventBus } from "../main.js";
export default {
  name: "character",
  props: ["character"],
  methods: {
    handleNameClick: function () {
      eventBus.$emit("selected-char", this.character);
    },
  },
};
</script>

<style>
</style>