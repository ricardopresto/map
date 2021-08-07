<template>
  <div id="main">
    <IconComponent 
    v-for="icon in iconlist" 
    :key="icon.index" 
    :image="icon.image" 
    @icon-click="$emit('icon-click', $event)"/>
  </div>    
</template>

<script>
import IconComponent from './IconComponent.vue';

export default {

  name: 'IconBox',

  components: {
    IconComponent
  },

  props: ['iconlist'],
}
</script>

<style scoped>
#main{
  width: 200px;
  height: 160px;
  display: flex;
  flex-flow: row wrap;
  background-color: var(--switcher-bg);
}
</style>