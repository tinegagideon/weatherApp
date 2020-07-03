<template>
  <div id="app">
    <header>
      <h1>WeatherApp</h1>
      <input
        type="text"
        autocomplete="off"
        class="search-box"
        placeholder="Search for a city..."
        v-model="query"
        @keypress="fetchWeather"
      />
    </header>

    <main class="card" v-if="typeof weather.main != 'undefined'">
      <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
      <div class="temp">{{ Math.round(weather.main.temp)}}°C</div>
      <div class="weather">{{weather.weather[0].main}}</div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "4b84c48893285fb922690f8ae9d5e5b5",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {}
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key === "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then(res => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  text-align: center;
  margin-top: 10em;
}
header h1 {
  font-size: 2.4em;
}
.search-box {
  padding: 0.2em;
  margin: 0.4em 0;
}
.card {
  font-size: 1.2em;
}
.card .weather {
  font-style: italic;
  font-weight: 600;
}
</style>
