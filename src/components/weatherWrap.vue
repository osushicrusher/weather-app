<template>
    <div class="weather-wrap"  v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
            <p class="location">{{ weather.name }}, {{ weather.sys.country }}</p>
            <p class="date">{{ showDate() }}</p>
        </div>
        <div class="weather-box">
            <p class="temp">{{ Math.round(weather.main.temp) }}&#8451;</p>
            <p class="temp-minmax">Min: {{ Math.round(weather.main.temp_min )}}&#8451; Max: {{ Math.round(weather.main.temp_max) }}&#8451;</p>
        </div>
    </div>
</template>

<script>
export default {

    props: ['weather'],
    name: 'weatherWrap',
    methods: {
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
    }
}
</script>

<style>

.weather-wrap {
    margin-top: 20px;
}

.location-box .location {
    color: #313131;
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
    color: #8f8e8e;
    font-size: 70px;
    font-weight: 900;
    background-color: #fff;
    border-radius: 16px;
    margin: 30px 0;
    box-shadow: 3px 6px rgba(0, 0, 0, .25);
}

.weather-box .temp-minmax {
    color: #FFF;
    font-size: 18px;
    font-style: italic;
    text-shadow: 0 0 12px rgba(0, 0, 0, .25);
}

.weather-box .weather {
    color: #FFF;
    font-size: 48px;
    font-weight: 700;
    font-style: italic;
    text-shadow: 3px 6px rgba(0, 0, 0, .25);
}
</style>