<script setup>
import { Head, Link } from '@inertiajs/vue3';
import axios from 'axios';
import { ref } from 'vue'

alert('input data provinsi dan kota -> tekan enter -> lalu ketik tombol apapun')
const queryProvince = ref('');
const queryCity = ref('');
var triggerCity = false;

var provinceName = "";
var cityName = "";
const weat = {
    weather: {},
    time: {},
    status: {},
    url_base: "https://cuaca-gempa-rest-api.vercel.app/weather/",
    // weather_icon: "http://openweathermap.org/img/wn/",
};

async function fetchWeatherProvince(e){
    if(e.key == "Enter"){
        provinceName = weat.url_base+queryProvince.value.replace(/ /g, '-').toLowerCase()
    }
}

async function fetchWeatherCity(e){
    // if(e.key == "Enter"){
        cityName = weat.url_base+queryProvince.value.replace(/ /g, '-').toLowerCase()+'/'+queryCity.value.replace(/ /g, '-').toLowerCase()
        if(!queryProvince.value == ""){
            triggerCity = true;
            axios.get(cityName)
            .then(response => {
                return response.data
            })
            .then(data => {
                weat.weather = data.data.params[2]
                weat.time = data.data.params[6]
                console.log(triggerCity)
            })
            .catch(err => {
                alert('check kembali nama provinsi dan kota')
            })
        }else{
            triggerCity = false;
            console.log('tidak ada data')
        }
    // }
}

</script>

<template>
    <Head title=""/>
    <div class="weather-container">
        <div class="weather-wrap">
            <div class="flex justify-between">
                <div class="search-box">
                    <!-- <h1>{{ weat.time }}</h1> -->
                    <input type="text" placeholder="Search by province" class="search-bar" 
                    v-model="queryProvince"/>
                </div>
                <div class="search-box">
                    <input type="text" placeholder="Search by city" class="search-bar" 
                    v-on:keyup.enter="fetchWeatherCity" v-model="queryCity"/>
                </div>
            </div>
            <div class="weather-info">
                <div class="location-box">
                    <div class="location">
                        <h1>{{ queryProvince ? queryProvince : 'Province name' }}, {{ queryCity ? queryCity : 'City name'  }}</h1>
                        <div v-if="triggerCity">
                            <!-- <li v-for="timess in weat.time.times">
                                <p> p{{ new Date((timess.datetime*1)+1511530605000) }}</p>
                                <p> {{ new Date((timess.datetime*1)+1511530605000) }}</p>
                            </li> -->
                            <h5>{{ new Date((weat.time.times[0].datetime*1)+1511532905000 )}}</h5>
                        </div>
                        <!-- <div class="date">{{ weat.time.times }}</div> -->
                        <div class="weather-box">
                            <div v-if="triggerCity">
                                <div class="temp">{{ weat.weather.times[0].celcius.replace(/ /g, '°').toLowerCase() }}</div>
                            </div>
                            <div v-else>
                                <div class="temp">0°</div>
                            </div>
                            <div class="weather">{{ triggerCity ? weat.time.times[0].name : 'Weather' }}</div>
                                <div class="icon">
                                    <img src=""/>
                                </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
