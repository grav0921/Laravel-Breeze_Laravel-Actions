<script setup>
import { Head, Link } from '@inertiajs/vue3';

const message ="";
const weat = {
    query: '',
    weather: {},
    url_base: "https://cuaca-gempa-rest-api.vercel.app/weather/",
    // weather_icon: "http://openweathermap.org/img/wn/",
};

const fetchWeather = (e) => {
    // if (e.key == "Enter"){
    //     let response = axios.get(
            
    //     )
    // }
}
</script>

<template>
    <Head title=""/>
    <h1>{{ weat.query }} asd</h1>
    <div class="weather-container">
        <div class="weather-wrap">
            <div class="search-box">
                <input type="text" placeholder="Search..." class="search-bar" 
                v-model="weat.query"/>
            </div>
            <p>Message is: {{ message }}</p>
            <input v-model="message" placeholder="edit me" />
            <!-- <div class="weather-info" v-if="typeof weather.main!=undefined'">
                <div class="location-box">
                <div class="location">{{weather.name}},{{weather.sys.country }}
            </div> -->
        </div>
    </div>
</template>
