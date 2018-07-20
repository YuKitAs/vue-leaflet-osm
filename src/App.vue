<template>
  <div id="app">
    <div id="map"></div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data: function() {
    return {
      map: null,
      tileLayer: null,
      layers: []
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

#map {
  height: 600px;
  width: 800px;
  border: 1px solid #AAA;
}
</style>
