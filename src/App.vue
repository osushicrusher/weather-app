<template>
    <div id="app" :class="weatherClass">
        <main>
            <searchBox @place="fetchWeather"></searchBox>
            <weatherWrap :weather="weather"></weatherWrap>
            <commentBox :weather="weather" :weatherImgUrl="weatherImgUrl"></commentBox>
        </main>
    </div>
</template>

<script>

import weatherWrap from './components/weatherWrap.vue'
import commentBox from './components/commentBox.vue'
import searchBox from './components/searchBox.vue'

export default {

  components: {
    weatherWrap,
    searchBox,
    commentBox,
  },

  name: 'app',
  data () {
    return {
      api_key: 'bcc8f92f1485d3839b6a5e3eacb98f1b',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
      weatherClass: '',
      weatherImgUrl: ''
    }
  },
  methods: {
    fetchWeather ($event) {
      this.query = $event
          fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults)
            .then(this.changeStyle)
    },
    setResults (results) {
      this.weather = results
    },
    changeStyle() {
      this.weatherClass = `${this.weather.weather[0].main}`.toLowerCase()
      this.weatherImgUrl = require('./assets/' + this.weather.weather[0].main.toLowerCase() + '.png')
    }
  }
}
</script>

<style>

.rain {
  background-image: linear-gradient(to bottom right, rgba(2, 2, 54, 0.8), rgba(5, 5, 122, 0.7));
}

.drizzle {
  background-image: linear-gradient(to bottom right, rgba(2, 2, 54, 0.8), rgba(5, 5, 122, 0.7));
}

.clear {
  background-image: linear-gradient(to bottom right, rgba(82, 82, 245, .8), rgba(109, 163, 243, .6));
}

.fog {
  background-image: linear-gradient(to bottom right, rgba(49, 48, 48, 0.541), rgba(203, 203, 206, 0.829));
  filter: blur(1px);
  -webkit-filter: blur(1px);
}

.clouds {
  background-image: linear-gradient(to bottom right, rgba(31, 30, 30, 0.644), rgba(203, 203, 206, 0.829));
}

.snow {
  background-color: rgb(206, 204, 204);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

main {
  min-height: 100vh;
  padding: 30px;
}
</style>
