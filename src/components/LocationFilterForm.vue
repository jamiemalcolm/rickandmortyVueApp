<template>
  <form>
    <input
      type="text"
      placeholder="search for location"
      v-model="search"
      v-on:keyup="searchForLocation"
    />
    <select v-on:change="handleLocationSelect" v-model="selectedLocation">
      <option default value="">Select A Location...</option>
      <option v-for="location in locations" :value="location">
        {{ location.name }}
      </option>
    </select>
  </form>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "location-filter-form",
  data() {
    return {
      search: "",
      selectedLocation: {},
    };
  },
  props: ["locations"],
  methods: {
    searchForLocation() {
      let foundLocation = this.locations.find((location) => {
        return (
          location.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1
        );
      });
      this.selectedLocation = foundLocation;

      eventBus.$emit("location-selected", this.selectedLocation);
    },

    handleLocationSelect() {
      this.search = "";
      eventBus.$emit("location-selected", this.selectedLocation);
    },
  },
};
</script>

<style>
</style>