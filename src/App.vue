<template>
  <div class="main">

    <div class="main__ipnut-box">
      <input v-on:keypress="fetchWeather" v-model="city" type="text" id="main__ipnut" placeholder="Weather in...">
    </div>

    <div class="main__weather-box" v-if="weather.main">
        <div class="date">{{ dateSetter() }}</div>
        <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
        <div class="temp">{{ Math.round(weather.main.temp-273.15) }}°c</div>
        <div class="weather">{{ weather.weather[0].main }}</div>
    </div>

  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return {
      key: 'bae0eeaad82ac5126b5cff66f664b9f8',
      city: '',
      weather: {}
    }
  },
  methods:{
    async fetchWeather(event){
      if(event.key === 'Enter'){
        const res = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.key}`);
        const weather = await res.json();
        this.weather = weather;
      }
    },
    dateSetter(){
      let d = new Date;
      let day = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];
      let month = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October',  'November', 'December'];
      return `${day[d.getDay()-1]}, ${d.getDate()} of ${month[d.getMonth()]}`
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Fjalla+One&display=swap');
*, *::after, *::before{
  box-sizing: border-box;
}

body{
  margin: 20px;
  padding: 0;
  background-image: radial-gradient(rgb(255, 255, 255), rgb(247, 247, 247), rgb(240, 240, 240), rgb(232, 232, 232), rgb(224, 224, 224), rgb(217, 217, 217), rgb(209, 209, 209), rgb(202, 202, 202), rgb(194, 194, 194), rgb(186, 186, 186), rgb(179, 179, 179), rgb(171, 171, 171));
  font-family: 'Fjalla One', sans-serif;
  color: #fff;
  text-align: center;
}

.main{
  width: 400px;
  height: 600px;
  margin: 0 auto;
  background-image: linear-gradient(to bottom right, rgb(111, 184, 252), rgb(103, 167, 250), rgb(94, 151, 248), rgb(86, 134, 246), rgb(78, 117, 244), rgb(69, 100, 242), rgb(61, 84, 240), rgb(52, 67, 238), rgb(44, 50, 236), rgb(36, 33, 234), rgb(27, 17, 232), rgb(19, 0, 230));
  box-shadow: 0 0 10px rgba(0,0,0,0.8);
  border-radius: 5px;
}

#main__ipnut{
  margin-top: 65px;
  width: 300px;
  height: 37px;
  border-radius: 15px;
  border: none;
  opacity: 0.8;
  padding-left: 15px;
}

#main__ipnut:active, :hover, :focus {
  outline: 0;
  outline-offset: 0;
}

.main__weather-box{
  font-size: 20px;
  margin-top: 80px;
}


</style>
