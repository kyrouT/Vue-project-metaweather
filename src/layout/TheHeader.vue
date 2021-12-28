<template>
  <div class="tophead">
      <h1>WeatherApp</h1>
  <img class="startingIcon" src="../assets/weather.png" alt="">
  </div>
  
      <form @submit.prevent="submitForm" class="bottomhead">
          <input @keypress.enter="search" type="text" placeholder="Type your City .... or your Coordinates to the next blocks " v-model="searched" >
          <input @keypress.enter="search" class="ll" :class="{invalid: !latt.isValid}" type="number" placeholder="lattitude" v-model="latt.val" @blur="clearValid('latt')">
          <input @keypress.enter="search" class="ll" :class="{invalid: !long.isValid}" type="number" placeholder="longitude" v-model="long.val" @blur="clearValid('long')">
          <button @click="search" class="searchbtn">Find Weather</button>
      </form>
      <p class="errorMsg" v-if="!formValid">{{errorMsg}}</p>
</template>

<script>
export default {
    data() {
        return {
            searched: "",
            latt: {
                val : 0,
                isValid: true
            },
            long:  {
                val : 0,
                isValid: true
            },
            coord:  {
                val : "",
                isValid: true
            },
            formValid: true,
            errorMsg: "" 
        }
    },
    methods: {
        clearValid(input) {
            this[input].isValid = true;
        },
        search() {
            this.formValid = true;
            if (this.searched != "" && (this.latt.val != 0 || this.long.val != 0)){
                this.formValid = false;
                this.errorMsg = ("You have to Enter only a Location or both the lattitude and longtitude");
            } else if (this.searched == "" && (this.latt.val == 0 || this.long.val == 0)) {
                this.formValid = false;
               this.errorMsg = ("You have to Enter only a Location or both the lattitude and longtitude");

            }else if (this.latt.val < -90 || this.latt.val > 90) {
                this.formValid = false;
                this.latt.isValid = false;
                this.errorMsg = "Lattitude value has to be between -90 and 90."
            }else if (this.long.val < -180 || this.long.val > 180) {
                this.formValid = false;
                this.long.isValid = false;
                this.errorMsg = "Longtitude value has to be between -180 and 180."
            }else if (this.latt.val != 0 && this.long.val != 0) {
                this.coord = this.latt.val + "," + this.long.val;
                this.$emit('searchCoord',this.coord) 
             } else {
                this.$emit('searchName',this.searched);   
            }
        }   
        
    }
}
</script>

<style scoped>
.invalid {
    border-color: red;
}
.errorMsg {
    color: red;
}
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