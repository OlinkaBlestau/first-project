<script>
import axios from "axios";

export default {
  data() {
    return {
      city: "",
      error: "",
      info: null,
    };
  },
  computed: {
    cityName() {
      return "'" + this.city + "'";
    },

    showTemp() {
      return "Temperature: " + this.info.main.temp;
    },
    showFeelsLike() {
      return "Feels like: " + this.info.main.feels_like;
    },
    showMinTemp() {
      return "Min temperature: " + this.info.main.temp_min;
    },
    showMaxTemp() {
      return "Max temperature: " + this.info.main.temp_max;
    },
  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "Need more than 1 symbol";
        return false;
      }

      this.error = "";
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=37d19ff7448566a5350530a52c605d6c`
        )
        .then((res) => (this.info = res.data));
    },
  },
};
</script>

<template>
  <div className="wrapper">
    <h1>Forecast weather</h1>
    <p>Forecast for {{ city == "" ? "your city" : cityName }}</p>
    <input v-model="city" type="text" placeholder="City" />
    <button v-if="city != ''" @click="getWeather()">Search</button>
    <p className="error">{{ error }}</p>
    <div v-if="info != null">
     <p>{{ showTemp }}</p>
        <p>{{ showFeelsLike }}</p>
        <p>{{ showMinTemp }}</p>
        <p>{{ showMaxTemp }}</p>
    </div> 
  </div>
</template>

<style scoped>
.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 20px;
  background: pink;
  padding: 20px;
  color: #d45c5c;
  text-align: center;
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
  border-bottom: 2px solid #fff;
  color: #612121;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}
.wrapper input:focus {
  border-bottom-color: #d45c5c;
}
.wrapper button {
  background: #fff;
  color: black;
  border-radius: 10px;
  border: 2px solid #fff;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}
</style>
