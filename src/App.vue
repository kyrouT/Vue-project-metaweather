<template>
  <the-header @search="search"> </the-header>
  <h1>Choose your location...</h1>
  <div class="locs">
    <locations class="loc"
    @picked="getWeather"
    @modalOff="modalToggle"
    v-for="loc in locations"
    :key="loc.woeid"
    :woeid="loc.woeid"
    :title="loc.title"
    :type="loc.location_type"
    :coords="loc.latt_long"
   ></locations>
  </div>

  <modal v-if="modalVisible" @click="modalToggle" :location="this.selectedLocation" :parent="this.parentLocation" :weather="this.weather" :dates="this.testing"></modal>
</template>

<script>
import axios from 'axios'
import TheHeader from './layout/TheHeader.vue'
import Modal from './components/Modal.vue'
import Locations from './components/Locations.vue'

export default {
  name: 'App',
  components: {
    Modal,
    TheHeader,
    Locations 
  },
  data() {
    return {
      weather:[],
      locations: [],
      modalVisible: false,
      test: this.$store.state.locs,
      selectedLocation: '',
      parentLocation: '',
      testing:{}
    }
  },
  created() {
    axios
      .get("https:/www.metaweather.com/api/location/search/?query=san")
      .then((response) => {
        this.locations = response.data;
        this.$store.state.locs = response.data;
      })
      .catch(error => {
        console.log(error.response);
      })
  },
  methods: {
    search(searched) {
      axios
      .get(`https:/www.metaweather.com/api/location/search/?query=${searched}`)
      .then((response) => {
        this.locations = response.data;
        this.$store.state.locs = response.data;
      })
      .catch(error => {
        console.log(error.response);
      })
    },
    getWeather(id) {
      this.modalToggle();
      axios 
      .get(`https://www.metaweather.com/api/location/${id}`)
      .then((response) => {
        this.weather = response.data.consolidated_weather[0];
        this.testing = response.data.consolidated_weather;
        this.parentLocation = response.data.title;
        this.selectedLocation = response.data.title;
      })
      .catch(error => {
        console.log(error.response);
      })
    },
    modalToggle() {
      this.modalVisible = !this.modalVisible;        
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.locs{
  display: flex;
  flex-wrap: wrap;
}

.loc{
  flex-basis: 500px;
  flex-grow: 1;
  
 
}

.loc:hover {
  opacity: 0.9;
  background-color: rgb(200, 206, 207);
  
}



</style>
