<template>
    <div id='iconholder'
      @click="$emit('icon-click', image)">
      <img :src="iconimage" />
    </div>
</template>

<script>
export default {
  name: 'Icon',
  props: ['image'],
  computed: {
    iconimage: function() {
      return require(`../../icons/${this.image}`);
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
  border: 1px solid red;
  width: 40px;
  height: 40px;
  background-repeat: no-repeat;
  background-position: center;
}
</style>