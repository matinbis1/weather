<template>
  <div class="wrapper">
    <h1>Погода сейчас</h1>
    <p>Узнать погоду в {{city == "" ? "вашем городе": city}}</p>
    <input type="text" v-model="city" placeholder="Введите ваш город">
    <button v-show="city != ''" @click="getWeather()">Узнать погоду</button>
    <p class="error">{{ error }}</p>
    <div v-if="info != null">
      <p>Температура: {{ info.main.temp }}</p>
      <p>Максимальная температура: {{ info.main.temp_max }}</p>
      <p>Минимальная температура: {{ info.main.temp_min }}</p>
    </div>
  </div>

</template>

<script>
import axios from "axios"
export default {
  data() {
    return {
      city: "",
      error: "",
      info: null
    }
  },
  methods: {
    getWeather(){
      if (this.city.trim().length < 2) {
        this.error = "Город не существует"
        return false
      }

      this.error = ""

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=0a788fd36cea70bd6ca16dc7d0c33393`)
        .then(res => (this.info = res.data))
    }
  }
}
</script>

<style scoped>

.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  background: rgb(75, 86, 145);
  padding: 20px;
  text-align: center;
  color: white;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid lightblue;
  color: azure;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus {
  border-bottom-color: blueviolet;
}

.wrapper button {
  background: yellow;
  color: rgb(170, 83, 12);
  border-radius: 10px;
  border: 2px solid orange;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}

.error {
  color: red;
}
</style>