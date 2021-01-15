<template>
  <div class="main-container">
    <h1>Rick And Morty</h1>
    <characters-list :characters="characters"></characters-list>
  </div>
</template>

<script>
import CharactersList from "./components/CharactersList.vue";
export default {
  name: "app",
  data() {
    return {
      characters: [],
      selectedCharacter: null,
    };
  },
  mounted() {
    this.getAllCharacters();
  },
  methods: {
    getAllCharacters: function () {
      fetch("https://rickandmortyapi.com/api/character?page=1")
        .then((res) => res.json())
        .then((data) => (this.characters = data.results));
    },
  },
  components: {
    "characters-list": CharactersList,
  },
};
</script>

<style>
</style>