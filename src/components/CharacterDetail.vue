<template>
  <div v-if="character">
    <div class="character-info">
      <li>
        <h2><span>Name :</span> {{ character.name }}</h2>
        <p><span>Species :</span> {{ character.species }}</p>
        <p><span>Origin :</span> {{ character.origin.name }}</p>
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
  },
};
</script>

<style scoped>
.character-info {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  text-align: center;
  background-color: purple;
  border-radius: 35px;
  width: fit-content;
  height: fit-content;
  padding: 20px;
}
img {
  border-radius: 35px;
}
</style>