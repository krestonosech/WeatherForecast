<script>
import axios from 'axios'
export default {
  data() {
    return {
      city: "",
      error: "",
      info:null
    }
  },
  computed: {
    cityName() {
      return this.city
    }
  },
  methods: {
  getWeather () {
    if (this.city.trim().length < 2) {
      this.error = "нужно нажать больше 1 символа"
      return false
    }
    this.error=""

    axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=9f2a83d114bbd32520d02b7f279221a2`)
    .then(res => (this.info = res.data))
  }
}
}
</script>

<template>
<div class="wrap">
  <h1>Погодное приложение</h1>
  <p>узнать погоду в {{city == "" ? "в вашем городе" : cityName }}</p>
  <input type="text" v-model="city" placeholder="введите город" name="" id="">
  <button v-if="city != ''" @click="getWeather()">получить погоду</button>
  <button disabled v-else>введите название города</button>
  <p class="error">{{ error }}</p>

  <p v-show="info !=null">{{ info }}</p>
</div>
</template>

<style>
.error {
  color: red;
}
.wrap {
  width: 900px;
  height: 500px;
  padding: 20px;
  text-align: center;
  color: black;
  border-radius: 50px;
  background-color: #fff;
}
.wrap h1 {
margin-top: 50px;
}
.wrap p {
  margin-top: 20px;

}
.wrap input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: black;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;

}
.wrap input:focus {
  border-bottom-color: red;
}
.wrap button:hover {
  transform: scale(1.1) translateY(-5px);
}
.wrap button {
  background-color: #0000e6;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #000099;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrap button:disabled {
  background-color: blueviolet;
  cursor: black;
}
</style>
