<template>
  <div v-if="location">
    <div class="location-info">
      <li>
        <h2>{{ location.name }}</h2>
        <p>{{ location.type }}</p>
      </li>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "location-details",
  data() {
    return {
      location: null,
    };
  },
  mounted() {
    eventBus.$on("location-selected", (location) => {
      this.location = location;
    });
  },
};
</script>

<style>
.location-info {
  /* display: flex; */
  /* flex-direction: row; */
  justify-content: space-around;
  text-align: center;
  background-color: purple;
  border-radius: 35px;
  padding: 20px;
}
</style>