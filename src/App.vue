<template>
  <div id="app">
    <div id="form">
      <input v-model="name" placeholder="Place name">
      <input v-model="lat" placeholder="Latitude [-90, 90]">
      <input v-model="lng" placeholder="Longitude [-180, 180]">
    </div>
    <div id="btn"><button @click="addMarker">Mark!</button></div>
    <div id="map"></div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data: function() {
    return {
      name: '',
      lat: null,
      lng: null,
      map: null,
      tileLayer: null
    }
  },
  mounted() {
    this.initMap()
    this.initLayers()
  },
  methods: {
    initMap() {
      this.map = L.map('map', {
        center: [50.0, 15.0],
        minZoom: 2,
        zoom: 2
      })
    },
    initLayers() {
      this.tileLayer = L.tileLayer('http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a>',
        maxZoom: 18
      }).addTo(this.map)
    },
    addMarker(e) {
      if (this.lat !== null && this.lng !== null) {
        if (this.validateCoord()) {
          L.marker([this.lat, this.lng]).bindPopup(this.name).addTo(this.map)
          this.clearInput(e)
        }
      }
    },
    validateCoord() {
      let valid = true
      let lat = this.lat
      let lng = this.lng

      if (isNaN(lat) || lat < -90 || lat > 90) {
        console.log("Invalid latitude: " + lat)
        valid = false
      }

      if (isNaN(lng) || lng < -180 || lng > 180) {
        console.log("Invalid longitude: " + lng)
        valid = false
      }

      return valid
    },
    clearInput(e) {
      this.name = ''
      this.lat = null
      this.lng = null

      e.preventDefault()
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#form {
  width: 600px;
  display: inline-flex;
  justify-content: space-between;
}

input {
  font-size: 16px;
}

#btn {
  margin-top: 10px;
}

button {
  height: 30px;
  width: 60px;
  font-size: 16px;
}

#map {
  height: 600px;
  width: 800px;
  border: 1px solid #AAA;
  margin: 20px auto;
}
</style>
