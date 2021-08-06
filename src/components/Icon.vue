<template>
    <div id='iconholder'
      @click="$emit('icon-click', image)">
      <img class="iconImage" :src="iconimage" />
    </div>
</template>

<script>
export default {
  name: 'Icon',
  props: ['image'],
  computed: {
    iconimage: function() {
      return require(`../assets/icons/${this.image}`);
    }
  },
  data() {
    return {

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