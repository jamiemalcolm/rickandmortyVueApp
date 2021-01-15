<template>
  <div class="characters-list">
    <h2>Characters:</h2>
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
.characters-list {
  background-color: purple;
  text-align: center;
  border-radius: 35px;
  padding: 20px;
}
</style>