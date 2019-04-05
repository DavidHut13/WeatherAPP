<template>
  <b-row>
    <b-col class="main">
      <div class="title text-center">
        <i class="fas fa-cloud fa-5x"></i>
        <span class="brand-name">Raindar</span>
        <h6>{{ this.name }}</h6>
      </div>
    </b-col>
  </b-row>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      temp: 20,
      location: {},
      crd: {},
      lat: "",
      long: "",
      name: "",
      weather: {}
    };
  },
  mounted() {
    this.promiseGetWeather();
    //this.getLocation();
    //this.axiosCall();
    //this.getWeather();
    
  },
  methods: {
     axiosCall() {
       axios
         .get('https://fcc-weather-api.glitch.me/api/current?lat=' + this.lat + '&lon=' + this.long)
         
         .then(res => {
     
           this.name = res.data.name;
           console.log(res);
         })
        .catch(err => {
           console.log(err)
         });
     },
    success(pos) {
      this.crd = pos.coords;
      this.lat = this.crd.latitude;
      this.long = this.crd.longitude;
      this.axiosCall();
    },
    // getLocation() {
    //   if (navigator.geolocation) {
    //     navigator.geolocation.getCurrentPosition(this.success);
    //   } else {
    //     this.location = "Geolocation is not supported by this browser.";
    //   }
    // },
     promiseGetWeather() {
      const imGettingTheWeather = new Promise ((resolve, reject) => {
        if (navigator.geolocation) {
          console.log('grabbing coordinates');
          navigator.geolocation.getCurrentPosition(this.success);
          //console.log(this.temp);
          resolve(console.log('got coordinates' + this.lat));
        }
         else {
        reject(new Error('fk error'));
    }
  });
      
        imGettingTheWeather 
        .then(() => {
          console.log('just finished grabbing coordinates')
          console.log(this.lat);
          // this.axiosCall();
        }, (error) => {
          console.log(error);
      });
    }
  }
}
</script>

<style scoped>
.title {
  font-family: "Fjalla One", sans-serif;
  color: white;
  top: 5%;
}

.main {
  margin: 0;
  padding: 0;
  height: 100vh;
  background-color: #353434;
}

.brand-name {
  font-size: 46px;
}
</style>
