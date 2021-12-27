<template>
  <div class="wrapper" @click="emitId">
      <!-- <location-card v-for="loc in locs" :key="loc.woeid" @modalOut="modalOff"></location-card> -->
      
      <h4>{{this.type}} of</h4>
      <h2>{{this.title}}</h2>
      <p>Located at {{this.coords}}.</p>
  </div>
</template>

<script>


export default {
    props: ['woeid','title','type','coords'],
    methods: {
        modalOff() {
            this.$emit('modalOff');
        },
        emitId() {
            console.log(this.title);
            this.$emit('picked',this.woeid);
        }
    },
    data() {
        return {
            locs : this.$store.state.locs
        }
    },
}
</script>

<style scoped>
    .wrapper{
        border: 1px solid black;
        border-radius: 10%;
    }

    ul {
        list-style: none;
       
        
    }
</style>