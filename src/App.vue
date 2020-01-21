<template>
  <div id="app">
    <Weather />
    <v-select :options="towns" v-model="selectedTown" v-on:input="changeHandler" style="width: 650px; margin: 0 400px"></v-select>
    <Days
        v-for="period of periods"
        v-bind:key = "period.number"
        v-bind:period = "period"
    />
  </div>
</template>
<script>
import Weather from '@/components/Weather'
import Days from '@/components/Days'
export default {
  data() {
    return {
        periods: [],
        towns: [{
            label: "Linn",
            coordinates: "39.7456,-97.0892"
        },
            {
            label: "New York",
            coordinates: "40.7283,-73.9942"
            }],
        selectedTown: {}
    }
  },
  mounted() {
    fetch(`http://geodb-free-service.wirefreethought.com/v1/geo/cities?countryIds=US&minPopulation=2500000&limit=10`)
            .then(response => response.json())
            .then(json => {
              this.towns = json.data.map(item => ({
                label: item.city,
                coordinates: `${item.latitude},${item.longitude}`
              }));
            });
  },
  methods: {
    changeHandler() {
      fetch(`https://api.weather.gov/points/${this.selectedTown.coordinates}`)
              .then(response => response.json())
              .then(json => {
                fetch(json.properties.forecast)
                        .then(response => response.json())
                        .then(forecastResp => {
                          this.periods = forecastResp.properties.periods
                        });
              })
    },
  },
  components: {
    Weather, Days
  },
}
</script>
<style>
    @import url('https://fonts.googleapis.com/css?family=Dancing+Script');
    @import url('https://fonts.googleapis.com/css?family=Comfortaa:300,400,700&display=swap');
    body {
      width: 100%;
      height: 100%;
      margin: 0;
      padding: 0;
      background: #F0F8FF;
    }
    h1 {
      margin: 0;
      text-align: center;
      color: white;
      text-shadow: black 0 0 1.5px;
      font-size: 40px;
      font-family: 'Dancing Script', cursive;
    }
    h2 {
      font-size: 30px;
      font-family: 'Comfortaa', cursive;
      margin: 5px 5px 5px 5px;
    }
    h3 {
      font-size: 22px;
      font-family: 'Comfortaa', cursive;
      text-align: justify;
      margin: 20px 20px 2px 2px;
    }
</style>