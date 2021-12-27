<template>
  <div class="wrapper" @click="emitId">
      <h4>{{this.type}} of</h4>
      <h2>{{this.title}}</h2>
      <p>Located at {{this.coords}}.</p>
      <p class="distance">{{this.distance}} km away from your Coordinates.</p>
  </div>
</template>

<script>


export default {
    props: ['woeid','title','type','coords','dist'],
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
    computed: {
        distance() {
            return this.$props.dist / 1000
        }
    }
}
</script>

<style scoped>
    .wrapper{
        border: 5px solid lightskyblue;
        border-radius: 5%;
    }

    ul {
        list-style: none;
       
        
    }
    .distance {
        color: grey;
        font-weight: bolder;
    }
</style>