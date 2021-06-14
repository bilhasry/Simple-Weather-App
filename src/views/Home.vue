<template>
  <div class="main-app">
    <div class="search">
      <img src="undraw_weather_app_i5sm.svg" alt="weather" title="weather"/>
      <h1>Know the Weather</h1>
      <p>
        Please kindly search your location to get the information about the weather
      </p>
      <div class="search-wrapper">
        <label for="search-input" class="search-label">
          Insert Your Location
        </label>
        <input
          type="text"
          name="search-input"
          v-model="searchTerm"
          @keyup="getLocationByQuery"
          class="search-input"
          placeholder="Your Location e.g Kuala Lumpur, Malaysia"
        />
        <ul>
          <li v-for="location in locationList" v-bind:key="location.place_id">
            <span
              @click="
                getWeather(
                  location.geometry.location,
                  location.formatted_address
                )
              "
            >
              {{ location.name }} - {{ location.formatted_address }}
            </span>
          </li>
        </ul>
      </div>
    </div>
    <WeatherCard
      :temperature="temperature"
      :address="address"
      :weather="weather"
      :active="showCard"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import WeatherCard from "@/components/WeatherCard.vue";
import axios from "axios";

let goolePlaceApiUrl = process.env.VUE_APP_PLACE_API_URL;
let googlePlaceApiKey = process.env.VUE_APP_PLACE_API_KEY;

console.log(googlePlaceApiKey);
export default {
  name: "Home",
  data() {
    return {
      searchTerm: "",
      locationList: {},
      address: "",
      weather: "",
      temperature: 0,
      showCard: false
    };
  },
  components: {
    WeatherCard
  },
  computed: {
    getLocationList: () => {
      return this.locationList;
    }
  },
  methods: {
    getLocationByQuery() {
      const vm = this;
      axios
        .get(
          `${goolePlaceApiUrl}?query=${this.searchTerm}&key=${googlePlaceApiKey}`
        )
        .then(function(response) {
          vm.locationList = response.data.results;
        });
    },
    getWeather(coordinate, address) {
      let weatherApiUrl = process.env.VUE_APP_WEATHER_API_URL;
      const weatherAPIKey = process.env.VUE_APP_WEATHER_API_KEY;

      var vm = this;
      axios
        .get(
          `${weatherApiUrl}lat=${coordinate.lat}&lon=${coordinate.lng}&appid=${weatherAPIKey}`
        )
        .then(response => {
          vm.weather = response.data.weather[0].description;
          vm.address = address;
          vm.temperature = response.data.main.temp - 273.15;
          vm.showCard = true;
        });
    }
  }
};
</script>

<style lang="less" scoped>
h1 {
  font-size: 1.875rem;
  line-height: 2rem;
  text-align: center;
  color: #fff;
}
.search {
  margin-top: 1rem;
  height: 476px;
  background-size: 100% auto;
  text-align: center;
  img {
    max-width: 50%;
    margin: 0px auto;
  }
  p {
    font-size: 0.75rem;
    color: #fff;
  }
  .search-label {
    display: none;
  }
  .search-wrapper {
    position: relative;
    ul {
      margin: 0px;
      padding: 0px;
      position: absolute;
      top: 88%;
      li {
        list-style: none;
        padding: 0.5rem;
        font-size: 0.75rem;
        background: #fff;
        border-bottom: 1px solid #efefef;
        cursor: pointer;
      }
    }
  }
  .search-input {
    width: 100%;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    padding: 1rem;
    font-size: 0.875rem;
    color: #fff;
    background: none;
    border: 1px solid #fff;
    display: block;
    border-radius: 0.5rem;
  }
}
</style>
