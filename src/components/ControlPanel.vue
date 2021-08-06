<template>
  <div id="main">
    <div id="switcher">
      <Switcher 
      @change-option="changeOption($event)"
      @capture="$emit('capture')"
      />
    </div>
    <div id="optionbox">
      <IconBox 
      v-if="active == 'icons'"
      :iconlist="iconlist"
      @icon-click="$emit('icon-click', $event)"
      />
      <LayerBox
      v-if="active == 'layers'"
      :layerlist="layerlist"
      @set-visible="$emit('set-visible', $event)"
      />
      <AddText
      v-if="active == 'text'"
      @add-text="$emit('add-text', $event)"
      />
      <Sizer
      v-if="active == 'size'"
      :mapWidth="mapWidth"
      :mapHeight="mapHeight"
      @height-change="$emit('height-change', $event)"
      @width-change="$emit('width-change', $event)"
       />
    </div>
  </div>
</template>

<script>
import IconBox from './IconBox.vue';
import LayerBox from './LayerBox.vue';
import AddText from './AddText.vue';
import Sizer from './Sizer.vue';
import Switcher from './Switcher.vue';

export default {
  name: 'ControlPanel',
  components: {
    IconBox,
    LayerBox,
    AddText,
    Sizer,
    Switcher
  },
  props: [ "mapWidth", "mapHeight", "layerlist", "iconlist" ],
  data() {
    return {
      active: 'icons'
    }
  },
  methods: {
    changeOption(newOption) {
      console.log(newOption);
      this.active = newOption;
    }
  }
}
</script>

<style scoped>
#main{
  position: absolute;
  display: flex;
  right: 20px;
  top: 20px;
  border: 1px solid white;
  border-radius: 6px;
}
#switcher{
  position: relative;
}
#optionbox{
  position: relative;
  top: 29px;
}
</style>
