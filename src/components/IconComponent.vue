<template>
  <div id="iconholder"
    @click="$emit('icon-click', image)">
    <img class="iconImage" :src="iconimage" 
    draggable 
    @dragstart="$emit('icon-dragged', image)"/>
  </div>
</template>

<script>
export default {

  name: 'IconComponent',

  props: ['image'],
  
  computed: {
    iconimage: function() {
      return require(`../assets/icons/${this.image}`);
    }
  }  
}
</script>

<style scoped>
#iconholder{
  width: 49px;
  height: 49px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.iconImage:hover{
  transform: scale(1.05);
}
</style>