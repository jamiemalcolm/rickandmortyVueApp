<template>
  <div class="outer-container">
    <h1>Rick And Morty</h1>
    <div class="main-container">
      <!-- <characters-list :characters="characters" class="list"></characters-list>
      <character-details :character="selectedCharacter"></character-details> -->
      <character-filter-form :characters="characters"></character-filter-form>
      <character-detail></character-detail>
    </div>
  </div>
</template>

<script>
import { eventBus } from "./main.js";
import CharactersList from "./components/CharactersList.vue";
import CharacterDetails from "./components/CharacterDetails.vue";

import CharacterFilterForm from "./components/CharacterFilterForm.vue";
import CharacterDetail from "./components/CharacterDetail.vue";
export default {
  name: "app",
  data() {
    return {
      characters: [],
      // selectedCharacter: null,
      locations: [],
      selectedLocation: null,
    };
  },
  mounted() {
    this.getAllCharacters();
    this.getLocations();

    eventBus.$on("selected-char", (character) => {
      this.selectedCharacter = character;
    });
  },
  methods: {
    getAllCharacters: function () {
      fetch("https://rickandmortyapi.com/api/character?page=1")
        .then((res) => res.json())
        .then((data) => (this.characters = data.results));
    },
    getLocations: function () {
      fetch("https://rickandmortyapi.com/api/location?page=1")
        .then((res) => res.json())
        .then((data) => (this.locations = data.results));
    },
  },
  components: {
    "characters-list": CharactersList,
    "character-details": CharacterDetails,
    "character-filter-form": CharacterFilterForm,
    "character-detail": CharacterDetail,
  },
};
</script>

<style>
body {
  color: limegreen;
  background-color: #9da2ab;
}
h1 {
  text-align: center;
}

.outer-container {
}
.main-container {
  display: flex;
  justify-content: space-evenly;
}
.list {
  justify-content: flex-start;
}
li {
  list-style: none;
}
</style>