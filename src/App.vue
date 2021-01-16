<template>
  <div class="outer-container">
    <h1>Rick And Morty</h1>
    <character-filter-form :characters="characters"></character-filter-form>
    <div class="main-container">
      <character-detail character="character"></character-detail>
    </div>
  </div>
</template>

<script>
import { eventBus } from "./main.js";
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
    this.getAllLocations();

    eventBus.$on("selected-location", (location) => {
      this.selectedLocation = location;
    });
  },
  methods: {
    getAllCharacters: function () {
      // create array from 1-671
      const array = [];
      for (var i = 0; i < 671; i++) {
        array.push(i + 1);
      }
      // map promise to an array of api fetch with character number taking the number from previous array
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

    getAllLocations: function () {
      const array = [];
      for (var i = 0; i < 108; i++) {
        array.push(i + 1);
      }
      const promises = array.map((number) => {
        return fetch(
          `https://rickandmortyapi.com/api/location/${number}`
        ).then((res) => res.json());
      });
      Promise.all(promises).then((data) => {
        const listOfLocations = data.reduce((location, locationToAdd) => {
          return location.concat(locationToAdd);
        }, []);
        return (this.locations = listOfLocations);
      });
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