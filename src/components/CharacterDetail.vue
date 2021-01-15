<template>
  <div v-if="character">
    <h2>{{ character.name }}</h2>
    <p>{{ character.species }}</p>
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "character-detail",
  data() {
    return {
      character: null,
    };
  },
  mounted() {
    eventBus.$on("character-selected", (character) => {
      this.character = character;
    });
  },
};
</script>

<style>
</style>