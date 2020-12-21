<template>
  <div class="about">
    
    <div class="weather">
      <ul>
        <li>{{ pref }}</li>
        <li>{{ city }}</li>
        <li>{{ town }}</li>
        <li>{{ allAddress }}</li>
      </ul>
      <p>{{ code }}</p>
      <!-- <h1 class="weather-title">Weather in {{ name }}</h1> -->
      <!-- <ul>
        <li>weather：{{ main }}</li>
        <li>temperature：{{ temp }}℃</li>
        <li>humidity：{{ humidity }}％</li>
        <li>wind speed：{{ speed }}m</li>
      </ul> -->
      <a @click="$router.push({ name: 'Home' })" class="cp_btn">button</a>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["zip"],
  data() {
    return {
      pref: "",
      city: "",
      town: "",
      allAddress: "",
      name: "",
      main: "",
      temp: "",
      humidity: "",
      speed: ""
    };
  },
  async created() {
    let code = await axios.get(
      `https://apis.postcode-jp.com/api/v4/postcodes/${this.zip}?apiKey=ZCxePaJWxCZcvFWy8cuRrA01Sca4rCOZ8HsGePl`, { 
        withCredentials: true
    });
    this.data = code.data;
    this.pref = this.data.pref;
    this.city = this.data.city;
    this.town = this.data.town;
    this.allAddress = code.allAddress;
    return { code: code };

    // let item = await axios.get(
    //   `https://api.openweathermap.org/data/2.5/weather?zip=${this.zip}&units=metric&appid=0744da2879733386661b061cd494b11d`
    // );
    // this.data = item.data;
    // this.name = this.data.name;
    // this.main = this.data.weather[0].main;
    // this.temp = this.data.main.temp;
    // this.humidity = this.data.main.humidity;
    // this.speed = this.data.wind.speed;
  }
};
</script>

<style scoped>
.about {
  width: 100vw;
  height: 100vh;
  background: url("https://coachtech-video.s3-ap-northeast-1.amazonaws.com/liane-metzler-Y1ByvAGQ5iE-unsplash+(1).jpg")
    no-repeat;
  background-size: cover;
  color: white;
}
.weather {
  width: 620px;
  margin: 0 auto;
  padding-top: 100px;
}
.weather-title {
  font-size: 64px;
}
.weather li {
  font-size: 24px;
  margin-top: 20px;
  margin-left: 30px;
}
.cp_btn {
  display: block;
  width: 600px;
  margin-top: 50px;
  padding: 10px;
  text-align: center;
  text-decoration: none;
  color: #ec407a;
  border: 2px solid #ec407a;
  border-radius: 3px;
  transition: 0.4s;
  cursor: pointer;
}
.cp_btn:hover {
  background: #ec407a;
  color: #fff;
}
</style>