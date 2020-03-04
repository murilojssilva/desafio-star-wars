<template>
  <div class="container">
    <h1>Planetas de Star Wars</h1>
    <StarWarsList :apiUrl="apiUrl" @setStarWarsUrl="setStarWarsUrl" />
  </div>
</template>

<script>
import StarWarsList from "./StarWarsList";
export default {
  name: "StarWars",
  data() {
    return {
      apiUrl: "https://swapi.co/api/planets/",
      StarWarsUrl: ""
    };
  },
  components: {
    StarWarsList
  }
};
</script>

<style scoped>
@import url("http://allfont.net/allfont.css?fonts=star-jedi");

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  background-image: url("https://www.itl.cat/pngfile/big/0-9431_star-star-wars-planets-background.jpg");

  font-family: "Star Jedi", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  font-family: "Star Jedi", arial;
  color: yellow;
}
</style>
