<template>
  <div class="locations-list">
    <h2>Locations:</h2>
    <location
      v-for="(location, index) in locations"
      :location="location"
      :key="index"
    ></location>
  </div>
</template>

<script>
import Location from "./Location.vue";

export default {
  name: "location-list",
  props: ["locations"],
  components: {
    location: Location,
  },
};
</script>

<style>
.locations-list {
  background-color: purple;
  text-align: center;
  border-radius: 35px;
  padding: 20px;
}
</style>