<template>
  <div class="tophead">
      <h1>WeatherApp</h1>
  <img class="startingIcon" src="../assets/weather.png" alt="">
  </div>
  
      <div class="bottomhead">
          <input @keypress="search" type="text" placeholder="Type your City .... or your Coordinates to the next blocks " v-model="searched" >
          <input class="ll" type="number" placeholder="lattitude" v-model="latt">
          <input class="ll" type="number" placeholder="longitude" v-model="long">
          <button @click="search" class="searchbtn">Find Weather</button>
      </div>
</template>

<script>
export default {
    data() {
        return {
            searched: "",
            latt: 0,
            long: 0,
            coord: "" 
        }
    },
    methods: {
        search() {
            if (this.searched != "" && (this.latt != 0 || this.long != 0)){
                console.log("You have to Enter only a Location or both the lattitude and longtitude");
            } else if (this.searched == "" && (this.latt == 0 || this.long == 0)) {
                console.log("You have to Enter only a Location or both the lattitude and longtitude");
            
            } else if (this.latt != 0 && this.long != 0) {
                this.coord = this.latt + "," + this.long;
                this.$emit('searchCoord',this.coord) 
            
            } else {
                this.$emit('searchName',this.searched);   
            }
        }   
        
    }
}
</script>

<style scoped>
.ll {
    width: 120px;
}

.bottomhead {
    margin-bottom: 30px;
}

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
    transition-duration: 0.3s;
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