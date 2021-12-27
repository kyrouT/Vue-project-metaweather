<template>
  <div class="wrapper" @click="emitId">
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
        border: 5px solid lightskyblue;
        border-radius: 5%;
    }

    ul {
        list-style: none;
       
        
    }
</style>