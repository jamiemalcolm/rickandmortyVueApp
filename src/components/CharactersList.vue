<template>
  <div>
    <p>This is the character list</p>
    <character
      v-for="(character, index) in characters"
      :character="character"
      :key="index"
    ></character>
  </div>
</template>

<script>
import Character from "./Character.vue";

export default {
  name: "characters-list",
  props: ["characters"],
  components: {
    character: Character,
  },
};
</script>

<style>
</style>