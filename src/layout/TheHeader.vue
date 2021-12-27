<template>
  <h1>WeatherApp</h1>
      <div>
          <input @keypress="search" type="text" placeholder="Enter City  or Coordinates..." v-model="searched">
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

h1 {
    font-size: 3em;
    color:darkblue;
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

</style>