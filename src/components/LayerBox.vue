<template>
  <div id='main'>
    <Layer 
    v-for="layer in layerlist"
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
  props: ['layerlist'],
}
</script>

<style scoped>
#main{
  display: flex;
  flex-direction: column;
  width: 200px;
  height: 200px;
  background-color: var(--switcher-bg);
  border: 1px solid black;
}
</style>