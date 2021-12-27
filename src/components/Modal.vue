<template>
  <div class="backModal">
      <div class="modal">
            <h1>{{location}}</h1>
            <h3>{{parent}}</h3>
           <p>{{ date0 }}</p>
           <img class="mainIcon" :src="this.iconUrl" alt="">     
           <div class="w_table">
               
                <table>
                    <tr>
                        <th>Temperature</th>
                        <td>{{this.$props.weather.the_temp}} &#xb0;C</td>
                        <th>Wind speed</th>
                        <td>{{this.$props.weather.wind_speed}} mph</td>
                    </tr>
                    <tr>
                        <th>Wind Direction</th>
                        <td>{{this.$props.weather.wind_direction_compass}} </td>
                        <th>Humidity</th>
                        <td>{{this.$props.weather.humidity}}%</td>
                    </tr>
                    <tr>
                        <th>Visibility</th>
                        <td>{{this.$props.weather.visibility}} miles</td>
                        <th>Predictability</th>
                        <td>{{this.$props.weather.predictability}}%</td>
                    </tr>
                </table> 
            
            </div> 

           
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
                return this.$props.weather.weather_state_name;
            }
               
    },
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
    max-width: 800px;
    height: 800px;
    align-items: center;
    justify-content: center;
    border-radius: 80%;
    border: 50px solid skyblue;
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
.mainIcon {
    height: 300px;
    width: 400px;
    margin-bottom: 20px;
}
.w_table {
    margin-left: 0px;
}
table, tr {
      border: 1px solid black;
}
th{
    text-align: start;
    padding-right: 10px;
}
td {
    text-align: center;
}


</style>