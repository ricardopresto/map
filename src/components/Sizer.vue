<template>
  <div id="main">
    <input type="range" min="20" max="600" v-model="setmapWidth" class="slider" id="width" @change="widthChange" >
    <span>Width: {{setmapWidth}}</span>
    <input type="range" min="20" max="800" v-model="setMapHeight" class="slider" id="height" @change="heightChange" >
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
      setMapHeight: this.mapHeight
    }
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
  border: 1px solid black;
  display: flex;
  flex-direction: column;
  background-color: var(--switcher-bg);
}
input{
  width: 180px;
  margin: 10px;
}
</style>