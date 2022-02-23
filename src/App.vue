<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 15 ? 'warm' : ''">
    <main>
      <div class="search-bar">
        <input type="text" name="" id="" class="search-area" placeholder="search..." v-model="query" @keypress="fetchWeather">
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="located-area">
            {{ weather.name }}, {{ weather.sys.country }} 
          </div>
          <div class="date">
            {{ dateTimeFormate() }}
          </div>
        </div>
        <div class="weather-box">
          <div class="temparature">{{ Math.round(weather.main.temp) }}°c</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>


export default {
  name: 'App',
 


 data(){
   return {
     api_key: 'fee8cd2f690be1557bdc7f33c30bcf7a',
     url_base: 'https://api.openweathermap.org/data/2.5/',
     query:'',
     weather:{}
   }
 },

  methods:{
     fetchWeather(e){
       if(e.key == "Enter"){
         fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`).then(res => {
           return res.json();
         }).then(this.setMyResult);
       }
     },


     setMyResult (results){
       this.weather = results;
     },


    dateTimeFormate(){
      let date = new Date();

      let month = ["January","February","March","April","May","June","July","August","September","October","November","December"];

      let day = ["Sun","Mon","Tue","Wed","Thu","Fri","Sat"];

      let myDay = day[date.getDay()];
      let myDate = date.getDate();
      let myMonth = month[date.getMonth()];
      let myYear = date.getFullYear();

      return `${myDay} ${myDate} ${myMonth} ${myYear}`;
    }
   }



}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Helvetica Neue",Helvetica;
}

#app {
  background-image: url('./assets/cold.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: bottom;
  transition: 0.7s;
}

#app.warm{
  background-image: url('./assets/warm.jpg');
}

main{
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.30), rgba(0,0,0,0.65));
}

.search-bar{
  width: 100%;
  margin-bottom: 30px;
}

.search-bar .search-area{
  display: block;
  width: 100%;
  padding: 20px;
  border: 1px solid #ffffff;
  border-radius: 50px;
  color: rgb(255, 255, 255);
  font-size: 20px;
  appearance: none;
  outline: none;
  background:transparent;
}

.location-box .located-area{
  color: #ffffff;
  font-size:32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0,0.30);
}

.location-box .date{
  color: #ffffff;
  font-size:17px;
  font-weight: 200;
  font-style: italic;
  text-align: center;
}

.weather-box{
  text-align: center;
}

.weather-box .temparature{
  display: inline-block;
  padding: 10px 25px;
  color: #ffffff;
  font-size: 130px;
  font-weight: 900;
  text-shadow: 3px 7px rgba(0,0,0,0.30);
  background-color: rgba(255,255,255,0.30);
  margin-top: 15px;
  border-radius: 25px;
  box-shadow: 5px 8px rgba(0,0,0,0.20);;
}

.weather-box .weather{
  color: #ffffff;
  font-size:50px;
  font-weight:600px;
  font-style: italic;
  text-shadow: 3px 7px rgba(0,0,0,0.30);
  margin-top: 20px;
}
</style>
