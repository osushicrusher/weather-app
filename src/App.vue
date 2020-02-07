<template>
  <div id="app" :class="bgChange()">
    <main>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined' ">
        <div class="location-box">
          <p class="location">{{ weather.name }}, {{ weather.sys.country }}</p>
          <p class="date">{{ showDate() }}</p>
        </div>
        <div class="weather-box">
          <p class="temp">{{ Math.round(weather.main.temp) }}&#8451;</p>
          <p class="temp-minmax">Min: {{ Math.round(weather.main.temp_min )}}&#8451; Max: {{ Math.round(weather.main.temp_max) }}&#8451;</p>
          <p>{{ weather.weather[0].main }}</p>
        </div>
      </div>
      <div class="search-box">
        <input 
        type="text" 
        class="search-bar" 
        placeholder="How will the weather be?" 
        v-model="query" 
        @keypress="fetchWeather"
        />
      </div>
      <div class="comment-box" v-if="typeof weather.main != 'undefined' ">
        <div class="icon-box">
          <img src="./assets/rain.png">
          <img :src="img_src">
        </div>
        <p class="comment">Lorem ipsum dolor sit amet consectetur adipisicing elit. Nisi similique dolorem id vel illum nostrum architecto reiciendis dignissimos, ipsa error.</p>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      api_key: 'bcc8f92f1485d3839b6a5e3eacb98f1b',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
      img_src: require(`./assets/clear.png`),
      icon: ["clear.png", "cloud.png", "drizzle.png", "rain.png"]
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults (results) {
      this.weather = results;
    },
    showDate() {
      const d = new Date();
      const months = [
        "January", "February", "March", "April", 
        "May", "June", "July", "August", "September", 
        "October", "November", "December"
      ];
      const days = [
        "Sunday", "Monday", "Tuesday", 
        "Wednesday", "Thursday", "Friday", "Saturday"
      ];

      const day = days[d.getDay()];
      const date = d.getDate();
      const month = months[d.getMonth()];
      const year = d.getFullYear();
      
      return `${day} ${date} ${month} ${year}`;
    },
    bgChange() {
      if(typeof this.weather.main != 'undefined') {
        return  `${this.weather.weather[0].main}`.toLowerCase();
        }
    },
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

.search-box {
  margin-top: 20px;
  width: 100%;
}

.search-box .search-bar {
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 21px;
  appearance: none;
  -webkit-appearance: none;
  border: none;
  outline: none;
  background: none;
  background-color: rgba(255, 255, 255, 0.75);
  box-shadow: 0 0 8px rgba(0, 0, 0, .2);
}

.search-box .search-bar:focus {
  box-shadow: 0 0 16px rgba(0, 0, 0, .2);
  background-color: rgba(255, 255, 255, .9);
}


.location-box .location {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, .25);
}

.location-box .date {
  color: #FFF;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 70px;
  font-weight: 900;
  text-shadow: 0 0 12px rgba(0, 0, 0, .75);
  background-color: rgba(255, 255, 255, .25);
  border-radius: 16px;
  margin: 30px 0;
  box-shadow: 3px 6px rgba(0, 0, 0, .25);
}

.weather-box .temp-minmax {
  color: #FFF;
  font-size: 18px;
  text-shadow: 0 0 12px rgba(0, 0, 0, .25);
}

.weather-box .weather {
  color: #FFF;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, .25);
}

.comment-box {
  background-color: #FFF;
  border-radius: 10px;
  box-shadow: 0 0 12px rgba(0, 0, 0, .75);
  display: flex;
  align-items: center;
  margin-top: 50px;
  width: 100%;
}

.icon-box {
  border-right: 3px solid #313131;
  padding: 10px;
  width: 30%;
}

.icon-box img {
  width: 100%;
  height: auto;
}

.comment {
  display: inline-block;
  padding: 20px;
  width: 70%;
}

</style>
