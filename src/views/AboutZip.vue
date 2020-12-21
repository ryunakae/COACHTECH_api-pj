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
    return { code: code }
  }
};
</script>