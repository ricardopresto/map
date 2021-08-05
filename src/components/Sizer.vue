<template>
  <div id="main">
    <input type="range" min="20" max="500" v-model="setWidth" class="slider" id="width" @change="widthChange" >
    <input type="range" min="20" max="500" v-model="setHeight" class="slider" id="height" @change="heightChange">
  </div>
</template>

<script>
export default {
  name: 'Sizer',
  props: ['mapWidth', 'mapHeight'],
  data() {
    return {
      setWidth: this.mapWidth,
      setHeight: this.mapHeight
    }
  },
  methods: {
    heightChange() {
      this.$emit('height-change', this.setHeight);
    },
    widthChange() {
      this.$emit('width-change', this.setWidth);
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