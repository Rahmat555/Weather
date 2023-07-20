<template>
<link href='https://fonts.googleapis.com/css?family=Rubik' rel='stylesheet'>
<div id="back">
    <div id="app">
        <div class="main1">
            <div v-if="data.weather">
              <span class="name_app">Weather application</span>
              <div class="header">
                <div class="temp">
                  <h2>{{Math.round(data.weather.main.temp)}}&deg;</h2>
                </div>
                <div class="city_box">
                  <h1>{{data.weather.name}}</h1>
                  <h3>{{ new Date().toLocaleString()}}</h3>
                </div>
                  <div class="state">
                    <div class="state_icon" v-if="state_weather == 0"><img src="../assets/cloud.png" alt=""></div>
                    <div class="state_icon" v-if="state_weather == 1"><img src="../assets/sun.png" alt=""></div>
                    <div class="state_icon" v-if="state_weather == 2"><img src="../assets/rain.png" alt=""></div>
                    <h3>{{ data.weather.weather[0].main}}</h3>
                  </div>
              </div>
            </div>
            <div class="search_box">
                <div class="search_form" id="search_form">
                    <input class="search_bar" type="text" placeholder="Another location" v-model="data.city" @keyup.enter="getApi()">
                    <button @click="getApi()" type="submit" class="search_button">
                        <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" width="30" height="30" viewBox="0 0 50 50">
                            <path d="M 21 3 C 11.621094 3 4 10.621094 4 20 C 4 29.378906 11.621094 37 21 37 C 24.710938 37 28.140625 35.804688 30.9375 33.78125 L 44.09375 46.90625 L 46.90625 44.09375 L 33.90625 31.0625 C 36.460938 28.085938 38 24.222656 38 20 C 38 10.621094 30.378906 3 21 3 Z M 21 5 C 29.296875 5 36 11.703125 36 20 C 36 28.296875 29.296875 35 21 35 C 12.703125 35 6 28.296875 6 20 C 6 11.703125 12.703125 5 21 5 Z"></path>
                        </svg>
                    </button>
                </div>
                <hr id="search_line">
                <div class="citys">
                    <ul class="ul_citys">
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Andijon')">Andijon</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Buxoro')">Buxoro</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Fargona')">Fargona</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Jizzakh')">Jizzakh</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Xiva')">Xiva</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Namangan')">Namangan</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Navoiy')">Navoiy</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Qashqadaryo')">Qashqadaryo</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Samarqand')">Samarqand</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Sirdaryo')">Sirdaryo</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Termiz')">Termiz</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Toshkent')">Toshkent</button></li>
                        <li class="li_citys"><button class="button_city" @click="getApi(this.data.city = 'Nukus')">Nukus</button></li>
                    </ul>
                    <hr class="citys_line">
                </div>
                <span class="span_detail">Weather Details</span>
                <div v-if="data.weather" class="weather_description">
                    <ul class="weather_details">
                      
                        <li class="li_weather">Cloudy</li><span class="span_weather">{{data.weather.clouds.all}}%</span>
                        <li class="li_weather">Humidity</li><span class="span_weather">{{data.weather.main.humidity}}%</span>
                        <li class="li_weather">Wind</li><span class="span_weather">{{data.weather.wind.speed}}km/h</span>
                        <li class="li_weather">Rain</li><span class="span_weather">{{data.weather.rain}}mm</span>
                      
                    </ul>
                    <hr class="weather_line">
                </div>
            </div>

        </div>

    </div>
</div>
</template>

<script>
import axios from "axios"
export default {
  name: 'weather',
  data(){
    return{
      data:{
        city:'',
        weather: null,
        current_day:'',
        state_weather:false
      }
    }
  },
  mounted: async function(){
      this.getApi()
  
  },
methods:{
   async getApi(){
    if(this.data.city===''){
      this.data.city = 'Tashkent'
    }
    const getWeather = await axios.get(`https://api.openweathermap.org/data/2.5/weather?units=metric&q=${this.data.city}&appid=261514ec6ead072a338a344dce0fb58f`)
    console.log(getWeather);
    this.data.weather = getWeather.data
    this.data.city = ''
    if(this.data.weather.weather[0].main == 'Clouds'){
      this.state_weather = 0
    }if(this.data.weather.weather[0].main == 'Clear'){
      this.state_weather = 1
    }if(this.data.weather.weather[0].main == 'Rain'){
      this.state_weather = 2
    }
            }
       }
    }
</script>


<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

#app {
    background-image: url(../assets/adventure.jpg);
    background-size: cover;
    background-position: bottom;
    max-width: 90%;
    max-height: 85%;
    margin: auto;

}
.temp{
  font-size: 60px;
  color: white;
  text-shadow: 3px 3px rgba(0,0,0,0.15);
  font-family: 'Rubik', sans-serif;
  font-weight: 300;
}
.city_box{
  font-family: 'Rubik', sans-serif;
  color: white;
  font-size: 16px;
  font-weight: 100;
  margin: 30px 10px 10px 30px;
  max-height: 100%;
}

.li_citys{
  margin: 20px 30px;
}

.ul_citys{
  display: block;
  overflow-y: scroll;
  height: 210px;

}

.citys_line{
  width: 55vh;
  margin-top: 3vh;
  margin-left: 2.5vh;
  color: aliceblue;
}

#search_line{
  width: 40vh;
  margin-left: 2.5vh;
  color: aliceblue;
}
.button_city{
  border: none;
  background: none;
  font-family: 'Rubik', sans-serif;
  color: white;
  font-size: 16px;
  font-weight: 100;
}
.button_city:hover{
  box-shadow: 0 12px 16px 0 rgba(0,0,0,0.24), 0 17px 50px 0 rgba(0,0,0,0.19);

}
#back {
    padding-top: 5%;
    padding-bottom: 5%;
    background-image: url(../assets/adventure2.jpg);
    background-size: cover;
    background-position: top;
}

.search_box {
    width: 35%;
    max-height: 100%;
    position: relative;
    background-color: black;
    opacity: 0.3;
    color: black;

}

.header{
  position: absolute;
  bottom: 0;
  left: 25vh;
  display: flex;
}

.search_form{
  display: flex;
}

.search_button {
    border: 0;
    width: 15vh;

}

.search_bar {
    background: none;
    border: none;
    color: black;
    width: 50vh;
    height: 12vh;
    padding-left: 35px;
    font-size: 14px;
    font-family: 'Rubik', sans-serif;
    color: rgb(183, 198, 211);
}
.state{
  font-family: 'Rubik', sans-serif;
  color: white;
  font-size: 15px;
  margin: 15px 0 0 15px;
}

.name_app{
  position: absolute;
  left: 15vh;
  margin-top: 5vh;
  font-family: 'Rubik', sans-serif;
  color: white;
  font-size: 16px;
}

.weather_details{
  margin: 10px 10px 10px 20px;
  font-family: 'Rubik', sans-serif;
  color: white;
  font-size: 16px;
  display: grid;
  grid-template-columns: 50% 50%;
  grid-row-gap: 5vh;
}

.citys{
  font-family: 'Rubik', sans-serif;
  color: white;
  font-size: 16px;
}

ul{
  text-decoration: none;
  list-style: none;
}
.weather_description{
  position: absolute;
  max-height: 100%;
  left: 0;
  right: 1vh;
  bottom: 7vh;
}

.li_weather{
  position: relative;
  width: auto;
}
.span_weather{
  position: relative;
  width: auto;
  justify-self: end;

}
.weather_line{
  position: absolute;
  width: 55vh;
  margin-top: 3vh;
  left: 2.5vh;
  color: aliceblue;

}

.span_detail{
  position: absolute;
  color: white;
  font-size: 22px;
  text-emphasis-color: white;
  text-decoration-color: white;
  margin: 55px 0 0 20px;
  
}

.main1 {
    min-height: 100vh;
    box-shadow: inset;
    color: black;
    display: flex;
    justify-content: end;
}
</style>
