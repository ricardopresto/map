<template>
  <div id="app">
    <div id="modal" v-if="modal">
      <div id="closer" @click="closeModal">
        <span>CLOSE</span>
      </div>
    </div>
    <div id="map" :style="mapStyle"></div>
    
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
      /> 
  </div>
</template>

<script>
import mapboxgl from 'mapbox-gl';
import html2canvas from 'html2canvas';
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
      mapWidth: 600,
      mapHeight: 800
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
        preserveDrawingBuffer: true
      });
      this.map.on('load', () => {
        this.completeLayerList = this.map.getStyle().layers;
      })
    },
    createMarker(type) {
      let icon = document.createElement('img');
      icon.src = this.getIconImage(type);
      let marker = new mapboxgl.Marker({element: icon, draggable: true});
      marker.setLngLat(this.map.getCenter());
      marker.addTo(this.map);
    },
    addTextMarker(text) {
      let textMarker = document.createElement('div');
      textMarker.innerHTML = text;
      let newTextMarker = new mapboxgl.Marker({element: textMarker, draggable: true});
      newTextMarker.setLngLat(this.map.getCenter());
      newTextMarker.addTo(this.map);
    },
    getIconImage(type) {
      return require(`./assets/icons/${type}`)
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
}
#app{
  display: flex;
}
#modal{
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: cornflowerblue;
  width: 100vw;
  height: 100vh;
  z-index: 3;
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
