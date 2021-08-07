<template>
  <div id="main">
    <div id="wrapper">
      <vue-slider
      :width=170
      :min=100
      :tooltip="'none'"
      :max="initialWidth" 
      v-model="setMapWidth" 
      @change="widthChange">
      </vue-slider>
      <span>Width: {{setMapWidth}}</span>
      <vue-slider 
      :width=170
      :min=100
      :tooltip="'none'" 
      :max="initialHeight" 
      v-model="setMapHeight" 
      @change="heightChange">
      </vue-slider>
      <span>Height: {{setMapHeight}}</span>
    </div>
  </div>
</template>

<script>
import VueSlider from 'vue-slider-component'
import 'vue-slider-component/theme/default.css'

export default {
  name: 'Sizer',
  components: {
    VueSlider
  },
  props: ['mapWidth', 'mapHeight', 'windowWidth', 'windowHeight'],
  data() {
    return {
      setMapWidth: this.mapWidth,
      setMapHeight: this.mapHeight,
      initialWidth: this.windowWidth,
      initialHeight: this.windowHeight
    }
  },
  methods: {
    heightChange() {
      this.$emit('height-change', this.setMapHeight);
    },
    widthChange() {
      this.$emit('width-change', this.setMapWidth);
    }
  }
}
</script>

<style scoped>
#main{
  width: 200px;
  height: 160px;
  display: flex;
  flex-direction: column;
  background-color: var(--switcher-bg);
}
span{
  color: white;
  font-size: 11pt;
  margin-bottom: 10px;
  cursor: default;
  display: block;
}
#wrapper{
  padding: 20px 0 0 15px;
}
</style>