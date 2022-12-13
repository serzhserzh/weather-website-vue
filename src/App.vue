<template>
 <div class="priv">
  <div class="wrapper">
  <h1>ПоGODа</h1>
  <hr>
    <div class="container">
      <div>
        <input type="text" v-model="city" placeholder="Введите город">
      <p v-if="err !=null" style="position:absolute; color: white; font-family: 'Monserat'; font-size: 30px;">Ваш город не найден:(</p>
      </div>
      <button @click="getWeather">Узнать погоду</button>
    </div>
    <h2 v-if="info !=null ">{{info.name}}</h2>  
    <div class="result">
      <p class="cel" v-if="info !=null ">{{info.main.temp}} °</p>
      <div class="qqq"></div>
      <p class="weather" v-if="info !=null ">{{info.weather[0]['description']}} <br>ощущается как {{info.main.feels_like}} ° </p>
      
    </div>
    <img class="qq" src="../src/assets/giphy.gif" width="300" >
    
  </div>
 </div>
</template> 

<script>
import axios, { AxiosHeaders } from 'axios'
  export default{
    data() {
      return {
        city: "",
        info: null,
        icon: null,
        err: null,
      }
    },
    methods: {
      getWeather1(){
        axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=3c8563067aec5168415e7fe47aaacf2e&lang=ru`)
        .then(
          res => {
          this.info = res.data 
          document.querySelector('.qqq').innerHTML = `<img src="https://openweathermap.org/img/wn/${this.info.weather[0]['icon']}@2x.png">`
          this.err = null
        },
        error => {
          this.err = error
          }
        )
        
      },
    },


    methods: {
      getWeather(){
        axios.get(` https://api.weather.yandex.ru/v2/informers`,{
  headers: {
    'X-Yandex-API-Key:': '493fee1e-ef67-470f-83d0-a81d1ba264bf'
  }
})
        .then(
          res => {
          this.info = res.data 
          document.querySelector('.qqq').innerHTML = `<img src="https://openweathermap.org/img/wn/${this.info.weather[0]['icon']}@2x.png">`
          this.err = null
        },
        error => {
          this.err = error
          }
        )
        
      },
    }
  }
</script>

<style>
.qq{
  position: absolute;
 top: 600px;
}
.weather{
 
  font-size: 40px;
  text-align: left;
  color: white;
}
hr{
  height: 2px;
  border: 0;
}
.result{
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}
h2{
  font-family: 'Montserrat';
  padding: 30px;
  font-size: 80px;
  font-weight: 600;
  color:white;
}
.priv{
  background-color: rgba(0, 75, 119, 0.6);
  width: 1200px;
  height: 100vh;
}
.cel{
 
  font-size: 80px;
  font-weight: 1000;
  color: white;
}
.wrapper{
  font-family: 'Monserat';
  width: 1200px;
  height: 800px;
  border-radius: 20px;
  text-align: center;
}
.wrapper h1{
  font-family: 'Montserrat';
  padding: 30px;
  font-size: 80px;
  font-weight: 600;
  color: white;
}
.container{
  
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  margin-top: 40px;
}
.wrapper input{
  width: 300px;
  height: 70px;
  padding: 14px;
  border: 0;
  border-radius: 7px;
  outline: 0;
  font-size: 30px;
  font-family: 'Monserat';
}


.wrapper button{
  width: 300px;
  height: 75px;
  font-size: 30px;
  font-family: 'Montserat';
  border: 0;
  border-radius: 7px;
  background-color: white;
  cursor: pointer;
  
}
.wrapper button:hover{
  background: rgb(0, 75, 119);
  scale: 0.95;
  transition-duration: 0.5s;
  color: white;
}
.wrapper input:focus{
  transition-duration: 0.5s;
  scale: 1.03;
}

</style>
