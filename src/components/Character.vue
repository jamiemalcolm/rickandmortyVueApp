<template>
  <div>
    <li>{{ character.name }}</li>
  </div>
</template>

<script>
export default {
  name: "character",
  props: ["character"],
};
</script>

<style>
</style>