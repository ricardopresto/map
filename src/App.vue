<template>
  <div id="app" @click="createMarker">
    <AddIcon />
    <div id="map"></div>
  </div>
</template>

<script>
import mapboxgl from 'mapbox-gl';
import AddIcon from './components/AddIcon.vue';

export default {
  name: 'App',
  components: {
    AddIcon
  },
  data() {
    return {
      access_token: 'pk.eyJ1IjoicmljYXJkb3ByZXN0byIsImEiOiJja3J1bmloMHEwYnY4MnBzNWt6b2x6eHBuIn0.zivT6cbQcLcAFl1Q8GW-QA',
      center: [5.483333, 51.433333],
      map: {},
    };
  },

  mounted() {
    this.createMap()
  },

  methods: {
    createMap() {
      mapboxgl.accessToken = this.access_token;
      this.map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/mapbox/streets-v11",
        center: this.center,
        zoom: 8,
      });
    },
    createMarker() {
      var el = document.createElement('div');
      el.className = 'marker';
      var marker = new mapboxgl.Marker({element: el, draggable: true})
      marker.setLngLat([5.483333, 51.433333])
      marker.addTo(this.map);
    }
  },
}

</script>

<style>
#map {
  width: 90vw;
  height: 90vh;
  border: 1px solid black;
}
.marker{
  width: 100px;
  height: 20px;
  border: 1px solid black;
}
</style>
