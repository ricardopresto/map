<template>
  <div id="app">
    <div id="modal" v-if="modal">
      <div id="closer" @click="closeModal">
        <span>CLOSE</span>
      </div>
    </div>
    <div id="map" :style="mapStyle" @click="mapClick"></div>
    
      <ControlPanel 
      @capture="capture"
      @height-change="heightChange"
      @width-change="widthChange"
      @set-visible="setVisible($event)"
      @icon-click="createMarker($event)"
      @add-text="addTextMarker($event)"
      :mapWidth="mapWidth"
      :mapHeight="mapHeight"
      :layerlist="layerlist"
      :iconlist="iconlist"
      :windowWidth="windowWidth"
      :windowHeight="windowHeight"
      :markerTextSize="markerTextSize"
      /> 
  </div>
</template>

<script>
import mapboxgl from 'mapbox-gl';
import html2canvas from 'html2canvas';
import { v4 as uuidv4 } from 'uuid';
import ControlPanel from './components/ControlPanel.vue'
import iconlist from './components/iconlist';
import layerlist from './components/layerlist';

export default {
  name: 'App',
  components: {
    ControlPanel
  },
  data() {
    return {
      access_token: 'pk.eyJ1IjoicmljYXJkb3ByZXN0byIsImEiOiJja3J1bmloMHEwYnY4MnBzNWt6b2x6eHBuIn0.zivT6cbQcLcAFl1Q8GW-QA',
      center: [5.483333, 51.433333],
      map: {},
      completeLayerList: [],
      iconlist: iconlist,
      layerlist: layerlist,
      modal: false,
      mapWidth: 0,
      mapHeight: 0,
      windowWidth: window.innerWidth,
      windowHeight: window.innerHeight,
      markerTextSize: 14
    };
  },

  mounted() {
    this.createMap();
    this.mapWidth = window.innerWidth;
    this.mapHeight = window.innerHeight;
  },

  methods: {
    createMap() {
      mapboxgl.accessToken = this.access_token;
      this.map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/mapbox/streets-v11",
        center: this.center,
        zoom: 8,
        preserveDrawingBuffer: true
      });
      this.map.on('load', () => {
        this.completeLayerList = this.map.getStyle().layers;
        this.map.resize();
      })
    },
    createMarker(type) {
      let name = `marker${uuidv4()}`;
      let icon = document.createElement('img');
      icon.src = this.getIconImage(type);
      icon.id = name;
      this[name] = new mapboxgl.Marker({element: icon, draggable: true});
      this[name].setLngLat(this.map.getCenter());
      this[name].addTo(this.map);
    },
    addTextMarker(textInfo) {
      this.markerTextSize = textInfo[1];
      let name = `marker${uuidv4()}`;
      let textMarker = document.createElement('div');
      textMarker.innerHTML = textInfo[0];
      textMarker.style.fontSize = `${this.markerTextSize}pt`
      textMarker.id = name;
      this[name] = new mapboxgl.Marker({element: textMarker, draggable: true});
      this[name].setLngLat(this.map.getCenter());
      this[name].addTo(this.map);
    },
    getIconImage(type) {
      return require(`./assets/icons/${type}`)
    },
    mapClick(event) {
      let name = event.target.id;
      if (name.substring(0, 6) == 'marker') {
        this[name].remove();
      }
    },
    setVisible(info) {
      for (let item of this.completeLayerList) {
          if (info[1] == false) {
            if (item.id.includes(info[0])) {
              this.map.setLayoutProperty(item.id, 'visibility', 'none');
            }
          } else {if (item.id.includes(info[0])) {
              this.map.setLayoutProperty(item.id, 'visibility', 'visible');
            }
          }
      }
    },
    capture() {
      let map = document.getElementById('map');
      this.modal = true;
      html2canvas(map).then(function(canvas) {
        let modal = document.getElementById('modal');
        modal.append(canvas);
      });
    },
    closeModal() {
      this.modal = false;
    },
    heightChange(newHeight) {
      this.mapHeight = newHeight;
    },
    widthChange(newWidth) {
      this.mapWidth = newWidth;
    }
  },
  computed: {
    mapStyle () {
      return {
        height: `${this.mapHeight}px`,
        width: `${this.mapWidth}px`
      }
    }
  }
}
</script>

<style>
* {
  margin: 0;
  Padding: 0;
  box-sizing: border-box;
  --switcher-bg: rgb(140, 176, 199);
  font-family: Arial, Helvetica, sans-serif;
}
#app{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: rgb(175, 206, 224);
}
#map{
  border: 1px solid white;
}
#modal{
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgb(175, 206, 224);
  width: 100vw;
  height: 100vh;
  z-index: 6;
}
#closer{
  position: absolute;
  top: 0;
  right: 0;
  color: white;
  padding: 30px;
  cursor: default;
}
</style>
