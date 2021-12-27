<template>
  <the-header> </the-header>

  <button @click="modalToggle">Show store</button>
  <h1>Locations</h1>
  <div class="locs">
    <locations
    @click="emitId"
    @modalOff="modalToggle"
    v-for="loc in locations"
    :key="loc.woeid"
    :woeid="loc.woeid"
    :title="loc.title"
    :type="loc.location_type"
    :coords="loc.latt_long"
   ></locations>
  </div>

  <modal v-if="modalVisible" @click="modalToggle"> Weather stuff </modal>
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
      locations: [],
      modalVisible: false,
      test: this.$store.state.locs
    }
  },
  created() {
    axios
      .get("https://www.metaweather.com/api/location/search/?query=san")
      .then((response) => {
        this.locations = response.data;
        this.$store.state.locs = response.data;
      })
      .catch(error => {
        console.log(error.response);
      })
  },
  methods: {
    emitId() {
      console.log(this.woeid);
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


</style>
