<template>
  <div class="outer-container">
    <h1>Rick And Morty</h1>
    <character-filter-form :characters="characters"></character-filter-form>
    <div class="main-container">
      <!-- <characters-list :characters="characters" class="list"></characters-list>
      <character-details :character="selectedCharacter"></character-details>
      <location-list :locations="locations"></location-list>
      <location-details :location="selectedLocation"></location-details> -->
      <character-detail character="character"></character-detail>
    </div>
  </div>
</template>

<script>
import { eventBus } from "./main.js";
// import CharactersList from "./components/CharactersList.vue";
// import CharacterDetails from "./components/CharacterDetails.vue";
import LocationList from "./components/LocationList.vue";
import LocationDetails from "./components/LocationDetails.vue";

import CharacterFilterForm from "./components/CharacterFilterForm.vue";
import CharacterDetail from "./components/CharacterDetail.vue";

export default {
  name: "app",
  data() {
    return {
      characters: [],
      // selectedCharacter: null,
      locations: [],
      // selectedLocation: null,
    };
  },
  mounted() {
    this.getAllCharacters();
    this.getLocations();

    eventBus.$on("selected-location", (location) => {
      this.selectedLocation = location;
    });
  },
  methods: {
    getAllCharacters: function () {
      const array = [];
      for (var i = 0; i < 671; i++) {
        array.push(i + 1);
      }
      const promises = array.map((number) => {
        return fetch(
          `https://rickandmortyapi.com/api/character/${number}`
        ).then((res) => res.json());
      });
      Promise.all(promises).then((data) => {
        const listOfCharacters = data.reduce((character, characterToAdd) => {
          return character.concat(characterToAdd);
        }, []);
        return (this.characters = listOfCharacters);
      });
    },

    getLocations: function () {
      fetch("https://rickandmortyapi.com/api/location?page=1")
        .then((res) => res.json())
        .then((data) => (this.locations = data.results));
    },
  },
  components: {
    "character-filter-form": CharacterFilterForm,
    "character-detail": CharacterDetail,
    // "location-list": LocationList,
    // "location-details": LocationDetails,
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