<template>
  <div id="main">
    <input type="range" min="20" :max="initialWidth" v-model="setmapWidth" class="slider" id="width" @change="widthChange" >
    <span>Width: {{setmapWidth}}</span>
    <input type="range" min="20" :max="initialHeight" v-model="setMapHeight" class="slider" id="height" @change="heightChange" >
    <span>Height: {{setMapHeight}}</span>
  </div>
</template>

<script>
export default {
  name: 'Sizer',
  props: ['mapWidth', 'mapHeight'],
  data() {
    return {
      setmapWidth: this.mapWidth,
      setMapHeight: this.mapHeight,
      initialWidth: 0,
      initialHeight: 0
    }
  },
  mounted() {
    this.initialWidth = this.mapWidth;
    this.initialHeight = this.mapHeight;
  },
  methods: {
    heightChange() {
      this.$emit('height-change', this.setMapHeight);
    },
    widthChange() {
      this.$emit('width-change', this.setmapWidth);
    }
  }
}
</script>

<style scoped>
#main{
  width: 200px;
  height: 200px;
  display: flex;
  flex-direction: column;
  background-color: var(--switcher-bg);
}
.slider{
  width: 180px;
  margin: 10px;
  appearance: none;
  border-radius: 8px;
}
span{
  color: white;
  font-size: 11pt;
  padding-left: 20px;
  cursor: default;

}
</style>