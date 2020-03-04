<template>
  <div id="app">
    <StarWars />
  </div>
</template>

<script>
import StarWars from "./components/StarWars.vue";

export default {
  name: "App",
  components: {
    StarWars
  }
};
</script>

<style>
@import url("https://use.fontawesome.com/releases/v5.8.2/css/all.css");
body {
  margin: 0;
  padding: 0;
}
</style>
