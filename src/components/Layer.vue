<template>
  <div id='layerbox' @click="setVisible">
    <span>{{ layerName }}</span>
  </div>
</template>

<script>

export default {
  name: 'Layer',
  props: ['layerID', 'layerName'],
  data() {
    return {
      visible: true
    }
  },
  methods: {
    setVisible() {
      this.visible = !this.visible;
      this.$emit("set-visible", [this.layerID, this.visible]);
    }
  }
}

</script>

<style scoped>
#layerbox{
  width: 140px;
  height: 20px;
  border: 1px solid red;
}
</style>