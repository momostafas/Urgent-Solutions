<template>
  <v-card>
    <v-row justify="center" align="center" class="weatherContainer">
      <v-col cols="9" dir="ltr" class="text-center">
        <p class="headline white--text">Just type the city name</p>
        <p class="subtitle-1 grey--text">You must spell it correctly</p>
        <v-row>
          <v-col class="inputCol" cols="9">
            <v-text-field
              @keyup.enter="findWetherData"
              v-model="city"
              light
              solo
            ></v-text-field>
          </v-col>
          <v-col class="inputCol" cols="3">
            <v-btn class="findBtn" @click="findWetherData" color="primary"
              >find</v-btn
            >
          </v-col>
        </v-row>
        <weatherContent v-if="weather.id != undefined" :weather="weather" />
      </v-col>
    </v-row>
    <v-snackbar v-model="snackbar">
      {{ error }}
    </v-snackbar>
  </v-card>
</template>

<script>
import weatherContent from "./weatherContent";
export default {
  components: {
    weatherContent
  },
  data() {
    return {
      position: {
        lat: null,
        lng: null
      },
      weather: {},
      snackbar: false,
      error: "",
      city: ""
    };
  },
  mounted() {
    this.getlocation();
  },
  methods: {
    /**
     * Get Location - gets the user`s current lat,lng position
     * @return {void}
     */
    getlocation() {
      navigator.geolocation.getCurrentPosition(pos => {
        this.position.lat = pos.coords.latitude;
        this.position.lng = pos.coords.longitude;
        this.getWetherData();
      });
    },
    /**
     * get Wether Data - get weather data from current location of user
     * @return {void}
     */
    getWetherData() {
      this.$http
        .get(
          "https://api.openweathermap.org/data/2.5/weather?lat=" +
            this.position.lat +
            "&lon=" +
            this.position.lng +
            "&APPID=4b8a06612d36cd6c6d5c14d587a3cd1b"
        )
        .then(res => {
          this.weather = res.data;
        })
        .catch(err => {
          this.error = err;
          this.snackbar = true;
          setTimeout(() => {
            this.snackbar = false;
          }, 6000);
        });
    },
    /**
     * findWetherData - get weather data from user input
     * @return {void}
     */
    findWetherData() {
      this.$http
        .get(
          "https://api.openweathermap.org/data/2.5/weather?q=" +
            this.city +
            ",{{country}&APPID=4b8a06612d36cd6c6d5c14d587a3cd1b"
        )
        .then(res => {
          this.weather = res.data;
        })
        .catch(err => {
          this.error = err;
          this.snackbar = true;
          setTimeout(() => {
            this.snackbar = false;
          }, 6000);
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.weatherContainer {
  height: 100vh;
  background-color: #26293a;
}

.findBtn {
  width: 100%;
  height: 48px !important;
  float: left;
  text-transform: capitalize;
}

.inputCol {
  padding: 0;
}
</style>
