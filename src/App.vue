<template>
  <div id="app">
    <div id="map"></div>
    <IconBox 
    :iconlist="iconlist"
    @icon-click="createMarker($event)"
    />
    <LayerBox
    :layers="layerlist"
    @set-visible="setVisible($event)"
    />
    <AddText
    @add-text="addTextMarker($event)"
    />
  </div>
</template>

<script>
import mapboxgl from 'mapbox-gl';
import IconBox from './components/IconBox.vue';
import LayerBox from './components/LayerBox.vue';
import AddText from './components/AddText.vue';
import iconlist from './components/iconlist';
import layerlist from './components/layerlist';

export default {
  name: 'App',
  components: {
    IconBox,
    LayerBox,
    AddText
  },
  data() {
    return {
      access_token: 'pk.eyJ1IjoicmljYXJkb3ByZXN0byIsImEiOiJja3J1bmloMHEwYnY4MnBzNWt6b2x6eHBuIn0.zivT6cbQcLcAFl1Q8GW-QA',
      center: [5.483333, 51.433333],
      map: {},
      completeLayerList: [],
      iconlist: iconlist,
      layerlist: layerlist
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
      return require(`../icons/${type}`)
    },
    setVisible(info) {
      console.log(info);
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
    }
  }
}

</script>

<style>
#app{
  display: flex;
}
#map {
  width: 70vw;
  height: 90vh;
  border: 1px solid black;
}
</style>
