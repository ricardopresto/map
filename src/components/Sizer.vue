<template>
  <div id="main">
    <input type="range" min="20" max="600" v-model="mapWidth" class="slider" id="width" @change="widthChange" >
    <input type="range" min="20" max="800" v-model="mapHeight" class="slider" id="height" @change="heightChange">
  </div>
</template>

<script>
export default {
  name: 'Sizer',
  props: ['mapWidth', 'mapHeight'],
  data() {
    return {
    }
  },
  methods: {
    heightChange() {
      this.$emit('height-change', this.mapHeight);
    },
    widthChange() {
      this.$emit('width-change', this.mapWidth);
    }
  }
}
</script>

<style scoped>
#main{
  width: 150px;
  height: 200px;
  border: 1px solid black;
}
</style>