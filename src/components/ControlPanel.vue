<template>
  <div>
    <IconBox 
      :iconlist="iconlist"
      @icon-click="$emit('icon-click', $event)"
      />
      <LayerBox
      :layerlist="layerlist"
      @set-visible="$emit('set-visible', $event)"
      />
      <AddText
      @add-text="$emit('add-text', $event)"
      />
      <Sizer
      :mapWidth="mapWidth"
      :mapHeight="mapHeight"
      @height-change="$emit('height-change', $event)"
      @width-change="$emit('width-change', $event)"
       />
  </div>
</template>

<script>
import IconBox from './IconBox.vue';
import LayerBox from './LayerBox.vue';
import AddText from './AddText.vue';
import Sizer from './Sizer.vue';

export default {
  name: 'ControlPanel',
  components: {
    IconBox,
    LayerBox,
    AddText,
    Sizer
  },
  props: [ "mapWidth", "mapHeight", "layerlist", "iconlist" ],
}
</script>

<style scoped>

</style>