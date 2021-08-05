<template>
  <div id='main'>
    <Layer 
    v-for="layer in layers"
    :key="layer.index"
    :layerID="layer.id"
    :layerName="layer.name"
    @set-visible="$emit('set-visible', $event)"
    />
  </div>
</template>

<script>
import Layer from './Layer.vue'

export default {
  name: 'LayerBox',
  components: {
    Layer
  },
  props: ['layers'],
}
</script>

<style scoped>
#main{
  width: 150px;
  height: 300px;
  margin-left: 10px;
  border: 1px solid black;
}
</style>