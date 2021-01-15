<template>
  <form>
    <select v-on:change="handleNameClick" v-model="selectedCharacter">
      <option disabled value="">Select A Character</option>
      <option v-for="character in characters" :value="character">
        {{ character.name }}
      </option>
    </select>
  </form>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "character-filter-form",
  data() {
    return { selectedCharacter: {} };
  },
  props: ["characters"],
  methods: {
    handleSelect() {
      eventBus.$emit("character-selected", this.selectedCharacter);
    },
  },
};
</script>

<style>
</style>