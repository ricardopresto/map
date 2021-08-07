<template>
  <div id="main">
    <LayerComponent 
    v-for="layer in layerlist"
    :key="layer.index"
    :layerID="layer.id"
    :layerName="layer.name"
    @set-visible="$emit('set-visible', $event)"
    />
  </div>
</template>

<script>
import LayerComponent from './LayerComponent.vue'

export default {

  name: 'LayerBox',

  components: {
    LayerComponent
  },

  props: ['layerlist'],
}
</script>

<style scoped>
#main{
  display: flex;
  flex-direction: column;
  width: 200px;
  height: 160px;
  background-color: var(--switcher-bg);
}
</style>