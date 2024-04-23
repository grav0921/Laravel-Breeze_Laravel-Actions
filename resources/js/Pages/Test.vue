<script setup>
import { Head, Link } from '@inertiajs/vue3';
import { ref } from 'vue'

const message ="";
const query = ref('');
const weat = {
    weather: {},
    url_base: "https://cuaca-gempa-rest-api.vercel.app/weather/",
    // weather_icon: "http://openweathermap.org/img/wn/",
};


</script>

<template>
    <Head title=""/>
    <div class="weather-container">
        <div class="weather-wrap">
            <div class="search-box">
                <input type="text" placeholder="Search" class="search-bar" 
                v-model="query"/>
            </div>
            <h1>Kota : {{ query }}</h1>
        </div>
    </div>
</template>
