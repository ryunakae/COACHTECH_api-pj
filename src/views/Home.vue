<template>
  <div class="home">
    <input type="number" v-model="zipcode" maxlength="7" minlength="7" />
    <button @click="getWeatherByZip()">Zip Code</button>
    <p>{{ allAddress }}</p>
    <div class="flex">
    <Card v-for="(data, index) in lists" :key="index" :city="data.city" />
    </div>
  </div>
</template>

<script>
import Card from "../components/Card";
import axios from "axios";

export default {
  data() {
    return {
      lists: [
        {
          city: "sapporo"
        },
        {
          city: "tokyo"
        },
        {
          city: "nagoya"
        },
        {
          city: "osaka"
        },
        {
          city: "fukuoka"
        },
        {
          city: "naha"
        }
      ],
      zipcode: "",
      allAddress: ""
    };
  },
  components: {
    Card
  },
  methods: {
    getWeatherByZip() {
      this.$router.push({ name: "AboutZip", params: { zip: this.zipcode} })
    }
  },
  async asyncData() {
    // let zipcode = '154-0024';
    let postcodeJp = await axios.get(
      `https://apis.postcode-jp.com/api/v4?postcode=3292763&apiKey=OAhDVYn8wbRNe9wWEL3NbgsYXZJpjejxsNIhO9x`
    );
    this.allAddress = postcodeJp.data.allAddress;
  }
};
</script>

<style scoped>
body {
  background: #eee;
}
.flex {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}
</style>