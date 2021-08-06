<template>
  <div id="main">
    <div id="icons" class="option" @click="$emit('change-option', 'icons')">
      <i class="fas fa-map-marker-alt icon"></i>
    </div>
    <div id="text" class="option" @click="$emit('change-option', 'text')">
      <i class="fas fa-font icon"></i>
    </div>
    <div id="layers" class="option" @click="$emit('change-option', 'layers')">
      <i class="fas fa-layer-group icon"></i>
    </div>
    <div id="size" class="option" @click="$emit('change-option', 'size')">
      <i class="fas fa-crop-alt icon"></i>
    </div>
    <div id="render" class="option" @click="$emit('capture')">
      <i class="fas fa-file-download icon"></i>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Switcher'
}
</script>

<style scoped>
#main{
  width: 200px;
  height: 30px;
  display: flex;
  flex-direction: row;
}
.option{
  width: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding-top: 2px;
  padding-left: 2px;
  background-color: var(--switcher-bg);
}
.icon{
  width: 20px;
  height: 20px;
  color: rgb(255, 255, 255);
}
#icons{
  border-radius: 6px 0 0 6px;
}
#render{
  border-radius: 0 6px 6px 0;  
}
</style>