<template>
  <div class="backModal">
      <div class="modal">
            <h1>{{location}}</h1>
            <h3>{{parent}}</h3>
           <p>{{ date0 }}</p>
           <img :src="this.iconUrl" alt="">
           <ul class="dates">
               <li v-for="date in dates" :key="date.id">
                    <img class="icons" :src="this.url+date.weather_state_abbr+this.svg"/>
                    <p>{{date.applicable_date}}</p>   
               </li>
           </ul>
      </div>
  </div>
</template>

<script>
export default {
    data() {
        return {
            url :"https://www.metaweather.com/static/img/weather/",
            svg :".svg" 
        }
    }    ,
    props:['location','parent','weather','dates'],
    computed: {
            iconUrl() {
                return this.url + this.$props.weather.weather_state_abbr + this.svg;
               
            },
            date0() {
                return this.$props.dates[0].weather_state_name;
            },      
    }
}
</script>

<style>

.backModal {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 99;
    background: rgba(0,0,0,0.5);
    display: flex;
    align-items: center;
    justify-content: center;
}

.modal {
    background: whitesmoke;
    padding: 150px;
    max-width: 350px;
    height: 80%;
    
    align-items: center;
    justify-content: center;
}

.dates {
    display: flex;
    list-style: none;
    align-items: center;
    justify-content: center;
    padding: 5px;

}
.icons {
    height: 100px;
    width: 100px;
}

</style>