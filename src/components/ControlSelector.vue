<template>
  <div id="main">
    <div id="icons" class="option" 
    @click="setIcons" v-bind:class="{ highlighted : iconsActive }">
      <i class="fas fa-map-marker-alt icon"></i>
    </div>
    <div id="text" class="option" 
    @click="setText" v-bind:class="{ highlighted : textActive }">
      <i class="fas fa-font icon"></i>
    </div>
    <div id="layers" class="option" 
    @click="setLayers" v-bind:class="{ highlighted : layersActive }">
      <i class="fas fa-layer-group icon"></i>
    </div>
    <div id="size" class="option" 
    @click="setSize" v-bind:class="{ highlighted : sizeActive }">
      <i class="fas fa-crop-alt icon"></i>
    </div>
    <div id="render" class="option" @click="$emit('capture')">
      <i class="fas fa-file-download icon"></i>
    </div>
  </div>
</template>

<script>
export default {
  
  name: 'ControlSelector',

  data() {
    return {
      iconsActive: true,
      textActive: false,
      layersActive: false,
      sizeActive: false
    }
  },

  methods: {
    setIcons() {
      this.$emit('change-option', 'icons');
      this.iconsActive = true;
      this.textActive = false;
      this.layersActive = false;
      this.sizeActive = false;
    },

    setText() {
        this.$emit('change-option', 'text');
        this.iconsActive = false;
        this.textActive = true;
        this.layersActive = false;
        this.sizeActive = false;
      },

    setLayers() {
      this.$emit('change-option', 'layers');
      this.iconsActive = false;
      this.textActive = false;
      this.layersActive = true;
      this.sizeActive = false;
    },
    
    setSize() {
      this.$emit('change-option', 'size');
      this.iconsActive = false;
      this.textActive = false;
      this.layersActive = false;
      this.sizeActive = true;
    },
  }
}
</script>

<style scoped>
#main{
  width: 200px;
  height: 30px;
  display: flex;
  flex-direction: row;
  background-color: rgb(140, 176, 199);
}
.option{
  width: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding-top: 2px;
  padding-left: 4px;
  background-color: var(--switcher-bg);
  border-radius: 6px;
  transition: 0.2s;
}
#icons{
  padding-left: 6px;
}
.option:hover{
  box-shadow: inset 0 0 5px white;
}
.highlighted{
  box-shadow: inset 0 0 5px white;
}
.icon{
  width: 20px;
  height: 20px;
  color: white;
}
</style>