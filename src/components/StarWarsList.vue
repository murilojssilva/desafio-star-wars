<template>
  <div class="list">
    <article v-for="(planet, index) in planets" :key="'plan' + index">
      <h3>{{ planet.name }}</h3>
      <p>
        <strong>Período de rotação</strong>
        : {{ planet.rotation_period }}
      </p>
      <p>
        <strong>Período orbital</strong>
        : {{ planet.orbital_period }}
      </p>
      <p>
        <strong>Diâmetro</strong>
        : {{ planet.diameter }}
      </p>
      <p>
        <strong>Clima</strong>
        : {{ planet.climate }}
      </p>
      <p>
        <strong>Gravidade</strong>
        : {{ planet.gravity }}
      </p>
      <p>
        <strong>Terreno</strong>
        : {{ planet.terrain }}
      </p>climate
    </article>
  </div>
</template>

<script>
export default {
  props: ["apiUrl"],
  data: () => {
    return {
      planets: [],
      nextUrl: "",
      currentUrl: ""
    };
  },
  methods: {
    fetchData() {
      let req = new Request(this.currentUrl);
      fetch(req)
        .then(resp => {
          if (resp.status === 200) return resp.json();
        })
        .then(data => {
          this.nextUrl = data.next;
          data.results.forEach(planet => {
            planet.id = planet.url
              .split("/")
              .filter(function(part) {
                return !!part;
              })
              .pop();
            this.planets.push(planet);
          });
        })
        .catch(error => {
          console.log(error);
        });
    },
    scrollTrigger() {
      const observer = new IntersectionObserver(entries => {
        entries.forEach(entry => {
          if (entry.intersectionRatio > 0 && this.nextUrl) {
            this.next();
          }
        });
      });

      observer.observe(this.$refs.infinitescrolltrigger);
    },
    next() {
      this.currentUrl = this.nextUrl;
      this.fetchData();
    },
    setStarWarsUrl(url) {
      this.$emit("setStarWarsUrl", url);
    }
  },
  created() {
    this.currentUrl = this.apiUrl;
    this.fetchData();
  },
  mounted() {
    this.scrollTrigger();
  }
};
</script>

<style scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 60%;
}
article {
  height: 100%;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  color: yellow;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
  cursor: pointer;
}
h3 {
  margin: 0;
}
</style>
