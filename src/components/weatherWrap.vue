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
    background-color: #fff;
    border-radius: 16px;
    box-shadow: 3px 6px rgba(0, 0, 0, .25);
    color: #313131;
    text-align: center;
    margin-top: 20px;
    padding: 20px;
}

.location-box {
    padding: 10px;
}

.location-box .location {
    font-size: 32px;
    font-weight: 500;
    text-shadow: 1px 3px rgba(0, 0, 0, .25);
}

.location-box .date {
    font-size: 20px;
    font-weight: 300;
    font-style: italic;
}

.weather-box {
    border: 2px solid #313131;
    padding: 10px;
}

.weather-box .temp {
    font-size: 70px;
    font-weight: 900;
    padding: 10px;
}

.weather-box .temp-minmax {
    font-size: 18px;
    font-style: italic;
    text-shadow: 0 0 12px rgba(0, 0, 0, .25);
    margin-top: 10px;
    padding: 10px;
}

</style>