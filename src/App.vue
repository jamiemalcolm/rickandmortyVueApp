<template>
  <div class="outer-container">
    <h1>Rick And Morty</h1>
    <div class="selects">
      <character-filter-form :characters="characters"></character-filter-form>
      <location-filter-form :locations="locations"></location-filter-form>
    </div>
    <div class="main-container">
      <character-detail character="character"></character-detail>
      <location-details location="location"></location-details>
    </div>
  </div>
</template>

<script>
import { eventBus } from "./main.js";
import LocationFilterForm from "./components/LocationFilterForm.vue";
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
    this.getAllLocations();
  },
  methods: {
    getAllCharacters: function () {
      fetch("https://rickandmortyapi.com/api/character?page=1")
        .then((res) => res.json())
        .then((data) => (this.characters = data.results));

      // // create array from 1-671
      // const array = [];
      // for (var i = 0; i < 1; i++) {
      //   array.push(i + 1);
      // }
      // // map promise to an array of api fetch with character number taking the number from previous array
      // const promises = array.map((number) => {
      //   return fetch(
      //     `https://rickandmortyapi.com/api/character/${number}`
      //   ).then((res) => res.json());
      // });
      // Promise.all(promises).then((data) => {
      //   const listOfCharacters = data.reduce((character, characterToAdd) => {
      //     return character.concat(characterToAdd);
      //   }, []);
      //   return (this.characters = listOfCharacters);
      // });
    },

    getAllLocations: function () {
      fetch("https://rickandmortyapi.com/api/location?page=1")
        .then((res) => res.json())
        .then((data) => (this.locations = data.results));
      // const array = [];
      // for (var i = 0; i < 1; i++) {
      //   array.push(i + 1);
      // }
      // const promises = array.map((number) => {
      //   return fetch(
      //     `https://rickandmortyapi.com/api/location/${number}`
      //   ).then((res) => res.json());
      // });
      // Promise.all(promises).then((data) => {
      //   const listOfLocations = data.reduce((location, locationToAdd) => {
      //     return location.concat(locationToAdd);
      //   }, []);
      //   return (this.locations = listOfLocations);
      // });
    },
  },
  components: {
    "character-filter-form": CharacterFilterForm,
    "character-detail": CharacterDetail,
    "location-filter-form": LocationFilterForm,
    "location-details": LocationDetails,
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
.selects {
  display: flex;
  flex-direction: row;
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