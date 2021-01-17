<template>
  <div class="outer-container">
    <div class="title">
      <h1>Rick And Morty</h1>
    </div>
    <div class="selects">
      <character-filter-form :characters="characters"></character-filter-form>
      <location-filter-form :locations="locations"></location-filter-form>
    </div>
    <div class="main-container">
      <character-detail character="character"></character-detail>
      <location-details location="location"></location-details>
    </div>
    <div class="favourite-list">
      <h2>Favourite Characters</h2>
      <p>
        add characters to your favourites by searching for a character and
        selecting 'add to favourites'
      </p>
      <div class="fav-list-item">
        <li v-for="character in favouriteCharacters">
          <img :class="small" v-bind:src="character.image" />
          <p>{{ character.name }}</p>
        </li>
      </div>
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
      // selectedFavourite: null,
      locations: [],
      // selectedLocation: null,
      favouriteCharacters: [],
    };
  },
  mounted() {
    eventBus.$on("character-to-save", (character) => {
      if (!this.favouriteCharacters.includes(character)) {
        this.favouriteCharacters.push(character);
      }
    });

    this.getAllCharacters();
    this.getAllLocations();
  },
  methods: {
    favouriteClicked: function () {
      eventBus.$emit("favourite-character-clicked", this.selectedFavourite);
    },

    getAllCharacters: function () {
      // create array from 1-671
      const array = [];
      for (var i = 0; i < 1; i++) {
        array.push(i + 1);
      }
      // map promise to an array of api fetch with character number taking the number from previous array
      const promises = array.map((number) => {
        return fetch(
          `https://rickandmortyapi.com/api/character/?page=${number}`
        ).then((res) => res.json());
      });
      Promise.all(promises).then((data) => {
        const listOfCharacters = data.reduce((character, characterToAdd) => {
          return character.concat(characterToAdd.results);
        }, []);
        return (this.characters = listOfCharacters);
      });
    },

    getAllLocations: function () {
      const array = [];
      for (var i = 0; i < 1; i++) {
        array.push(i + 1);
      }
      const promises = array.map((number) => {
        return fetch(
          `https://rickandmortyapi.com/api/location/?page=${number}`
        ).then((res) => res.json());
      });
      Promise.all(promises).then((data) => {
        const listOfLocations = data.reduce((location, locationToAdd) => {
          return location.concat(locationToAdd.results);
        }, []);
        return (this.locations = listOfLocations);
      });
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
@import url("https://fonts.googleapis.com/css2?family=Shadows+Into+Light&display=swap");
body {
  font-family: "Shadows Into Light", cursive;
  font-size: larger;
  color: #706c61;
  background-color: #afece7;
}
.title {
  background-image: url("https://media.istockphoto.com/vectors/retro-hippie-style-psychedelic-landscape-with-mountains-sun-and-the-vector-id1166455094?k=6&m=1166455094&s=612x612&w=0&h=v9bYMkx0A_-ahd4BzHLl0mRNE2IUqSwUQdVkAGb4IIo=");
  background-size: 20%;
  background-repeat: center;
  border-radius: 100%;
}
h1 {
  font-size: 400%;
  text-align: center;
  color: #1e2d24;
}
.selects {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.main-container {
  display: flex;
  justify-content: space-between;
}
.list {
  justify-content: flex-start;
}
li {
  text-decoration: solid;
  list-style: none;
}
img {
  border-radius: 35px;
  height: 100px;
  width: 100px;
}
.favourite-list {
  text-align: center;
}
.fav-list-item {
  display: flex;
  justify-content: space-evenly;
  width: fit-content;
  border-radius: 20px;
  padding: 40px;
}
</style>