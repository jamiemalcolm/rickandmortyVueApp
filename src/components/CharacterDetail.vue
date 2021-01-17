<template>
  <div v-if="character">
    <div class="character-info">
      <li>
        <h2><span>Name :</span> {{ character.name }}</h2>
        <p><span>Species :</span> {{ character.species }}</p>
        <p v-if="character.type"><span>Type :</span> {{ character.type }}</p>

        <p><span>Origin :</span> {{ character.origin.name }}</p>
        <p><span>Status :</span> {{ character.status }}</p>
        <p><span>Gender :</span> {{ character.gender }}</p>
        <form v-on:submit.prevent="saveCharacter">
          <input type="submit" value="Add to Favourites" />
        </form>
        <!-- <p><span>Appears in </span>:{{ character.episode }}</p> -->
      </li>

      <img v-bind:src="character.image" />
      <!-- <button v-on:click="getEpisodesIn">Appears In</button> -->
    </div>
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
  methods: {
    getEpisodesIn: function () {},

    saveCharacter: function () {
      eventBus.$emit("character-to-save", this.character);
    },
  },
};
</script>

<style scoped>
.character-info {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  text-align: center;
  background-color: #81f499;
  border-radius: 35px;
  width: fit-content;
  height: fit-content;
  padding: 20px;
}
img {
  border-radius: 35px;
  height: 250px;
  width: 250px;
}
</style>