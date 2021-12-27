<template>
  <div class="tophead">
      <h1>WeatherApp</h1>
  <img class="startingIcon" src="../assets/weather.png" alt="">
  </div>
  
      <div>
          <input @keypress="search" type="text" placeholder="Type your City  or Coordinates and press Enter..." v-model="searched">
          <button @click="search" class="searchbtn">Find Weather</button>
      </div>
</template>

<script>
export default {
    data() {
        return {
            searched: ""
        }
    },
    methods: {
        search() {
            this.$emit('search',this.searched);
        }
    }
}
</script>

<style scoped>
.tophead {
    display: flex;
    align-items: top;
    justify-content: center;
}

h1 {
    font-size: 3em;
    color:darkblue;
}

button {
    background-color: lightskyblue;
    color: white;
    font-weight: bolder;
    font-size: 1.1em;
}

input {
    width: 70%;
    height: 60px;
    font-size: 1.5em;
    margin-right: 5px;
}

.searchbtn {
    height: 60px;
    
}

.startingIcon {
    height: 5%;
    width: 5%;
    min-width: 60px;
    min-height: 60px;
}

</style>