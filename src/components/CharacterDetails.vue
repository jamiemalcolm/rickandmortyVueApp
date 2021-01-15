<template>
  <div v-if="character">
    <div class="character-info">
      <li>
        <h2>{{ character.name }}</h2>
        <p>{{ character.species }}</p>
        <p>{{ character.type }}</p>
      </li>
      <img v-bind:src="character.image" />
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "character-details",

  props: ["character"],
};
</script>

<style>
.character-info {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  text-align: center;
  background-color: purple;
  border-radius: 35px;
  width: 500px;
  height: 300px;
  padding: 20px;
}
img {
  border-radius: 35px;
}
</style>