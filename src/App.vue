// :class=[weather.weather[0].description]
<template>
  <div id="app"  >
    <main>
      <div class="header">
        <h1>Weather App</h1>
      </div>
      <div class="search">
        <input
          type="text"
          class="search-input"
          placeholder="Chercher une ville..."
          v-model="query"
          @keypress="fetchWeather"
          autofocus
        />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="weather-location">
          <div class="location">
            {{ weather.name }},
            {{ weather.sys.country }}
          </div>
          <div class="date">
            {{ dateBuilder() }}
          </div>
        </div>
        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
          <div class="weather">{{ weather.weather[0].description }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import dayjs from "dayjs";
import locale from "dayjs/locale/fr";
dayjs().format();

export default {
  name: "App",
  data() {
    return {
      api_key: "377bd05104b45af3c31fa96e1535b815",
      url_base: "https://api.openweathermap.org/data/2.5/",
      lang: "fr",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(event) {
      if (event.key === "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}&lang=${this.lang}`
        )
          .then((response) => {
            return response.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
    dateBuilder() {
      let currentDate = dayjs()
        .locale(locale)
        .format("DD MMMM YYYY");
      return `${currentDate}`;
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Rock+Salt&display=swap');

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-image: url('./assets/images/landscape-1844230_1280.png');
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}
#app {
  height: 100vh;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-weight: bold;
}
.header {
  text-align: center;
  font-family: 'Rock Salt', cursive;
  font-size: 1.5rem;
}
.search {
  display: flex;
  justify-content: center;
  padding: 3rem;
}
.search-input {
  width: 50%;
  font-size: 2rem;
  padding: 1rem;
  border-radius: 20px;
  border: none;
  box-shadow: inset 5px 5px 15px 5px rgba(0,0,0,0.22);
}
.search-input:focus {
  outline-style: none;
  box-shadow: inset 5px 5px 15px 5px rgba(0,0,0,0.44);
}
.weather-wrap {
  display: flex;
  flex-direction: column;
  font-size: 3rem;
  text-align: center;
  height: 50vh;
}
.weather-wrap div {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  height: 50%;
}
</style>
